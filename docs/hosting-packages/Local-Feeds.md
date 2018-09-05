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
# <a name="local-feeds"></a>Yerel akışlar

Yerel NuGet paketi akışlar, paketleri yerleştireceğiniz yerel ağınızda (veya hatta yalnızca kendi bilgisayar) yalnızca hiyerarşik klasör yapılardır. Bu akışları sonra CLI, Paket Yöneticisi UI ve Paket Yöneticisi konsolu kullanarak tüm diğer NuGet işlemleri ile paket kaynağı olarak kullanılabilir.

Kaynak etkinleştirmek için yol ekleyin (gibi `\\myserver\packages`) kullanarak kaynakları listesine [Paket Yöneticisi UI](../tools/package-manager-ui.md#package-sources) veya [ `nuget sources` ](../tools/cli-ref-sources.md) komutu.

> [!Note]
> Hiyerarşik klasör yapılarını içinde NuGet 3.3 + desteklenir. Yalnızca performans hiyerarşik yapıda çok daha düşük olan paketleri içeren tek bir klasör Nuget'in önceki sürümlerini kullanın.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Başlatma ve hiyerarşik klasör koruma

Hiyerarşik tutulan klasörü ağacında, aşağıdaki genel yapıya sahiptir:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

Kullanırken NuGet bu yapı otomatik olarak oluşturur. [ `nuget add` ](../tools/cli-ref-add.md) akışa bir paket kopyalamak için komut:

```cli
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

`nuget add` Komutu ile tek bir pakette birden çok paket ile bir akış ayarlarken bilinmelidir bir zaman çalışır.

Böyle durumlarda kullanmak [ `nuget init` ](../tools/cli-ref-init.md) çalıştırdıysanız gibi tüm paketleri akışa bir klasöre kopyalamak için komut `nuget add` her birinde tek tek. Örneğin, aşağıdaki komutu tüm paketleri kopyalar `c:\packages` hiyerarşik bir için `\\myserver\packages`:

```cli
nuget init c:\packages \\myserver\packages
```

Olduğu gibi `add` komutu `init` olan uygun paket her biri içeren bir sürüm numarası klasörü içinde her paket tanımlayıcı için bir klasör oluşturur.
