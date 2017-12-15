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
# <a name="local-feeds"></a>Yerel akışları

Yerel NuGet paketi akışları yalnızca hiyerarşik klasör yapılarınızı paketleri yerleştirin, yerel ağınızda (veya hatta yalnızca kendi bilgisayarınızı) var. Bu Özet akışlarını CLI, Paket Yöneticisi kullanıcı Arabirimi ve Paket Yöneticisi konsolu kullanılarak tüm diğer NuGet işlemleriyle sonra paket kaynağı olarak kullanılabilir.

Kaynak sağlamak için kendi pathname ekleyin (gibi `\\myserver\packages`) kullanarak kaynaklarının listesi için [Paket Yöneticisi kullanıcı Arabirimi](../tools/package-manager-ui.md#package-sources) veya [ `nuget sources` ](../tools/cli-ref-sources.md) komutu.

> [!Note]
> Hiyerarşik klasör yapılarınızı NuGet içinde 3.3 + desteklenir. NuGet eski sürümleri yalnızca performans hiyerarşik yapıda çok daha az paketleri içeren tek bir klasör kullanın.

## <a name="initializing-and-maintaining-hierarchical-folders"></a>Başlatma ve hiyerarşik klasörleri koruma

Hiyerarşik sürümlü klasör ağacında aşağıdaki genel yapıya sahiptir:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          └─<other files>

Kullandığınızda NuGet bu yapı otomatik olarak oluşturur. [ `nuget add` ](../tools/cli-ref-add.md) bir paket akışa kopyalamak için komut:

```
nuget add new_package.1.0.0.nupkg -source \\myserver\packages
```

`nuget add` Komutu, bir seferde birden çok paket ile bir akış ayarlarken bilinmelidir bir paketi ile çalışır.

Bu gibi durumlarda kullanmak [ `nuget init` ](../tools/cli-ref-init.md) çalıştırdıysanız gibi tüm paketler akışa bir klasöre kopyalamak için komut `nuget add` her birinde tek tek. Örneğin, aşağıdaki komut tüm paketleri kopyalar `c:\packages` hiyerarşik bir için `\\myserver\packages`:

```
nuget init c:\packages \\myserver\packages
```

İle `add` komutu, `init` uygun paketi olan her biri içeren bir sürüm numarası klasör içinde her paket tanımlayıcısı için bir klasör oluşturur.
