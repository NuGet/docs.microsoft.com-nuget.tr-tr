---
title: Yerel NuGet paketleri oluşturma
description: C++ projelerinde kullanılmak üzere, yönetilen kod yerine C++ kodu içeren yerel NuGet paketleri oluşturma hakkında ayrıntılar.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 2a95fca2ce5496512627e913273e5b66128e34c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774204"
---
# <a name="creating-native-packages"></a>Yerel paketler oluşturma

Yerel bir paket yönetilen derlemeler yerine yerel ikili dosyalar içerir ve bu, C++ (veya benzer) projelerinde kullanılmasına izin verir. (Bkz. kullanım bölümündeki [Yerel C++ paketleri](../consume-packages/finding-and-choosing-packages.md#native-c-packages) .)

Bir C++ projesinde tüketilebilir olması için, bir paketin çerçeveyi hedeflemesi gerekir `native` . Mevcut olduğunda, NuGet tüm C++ projelerini aynı şekilde ele aldığı için bu Framework ile ilişkili herhangi bir sürüm numarası değildir.

> [!Note]
>  `<tags>` `.nuspec` Diğer geliştiricilerin bu etiketi arayarak paketinizi bulmasını sağlamak için, ' ın bölümüne yerel ' i eklediğinizden emin olun.

`native`Daha sonra, ve klasörlerinde dosyaları sağlayan yerel NuGet paketleri `\build` , `\content` `\tools` `\lib` Bu durumda kullanılmaz (NuGet bir C++ projesine doğrudan başvuru ekleyemez). Bir paket ayrıca `\build` , NuGet 'in paketi kullanan projelere otomatik olarak aktarılacağı hedefleri ve props dosyalarını da içerebilir. Bu dosyalar, `.targets` ve/veya uzantılarına sahip paket kimliğiyle aynı ada sahip olmalıdır `.props` . Örneğin, [cpprestsdk](https://nuget.org/packages/cpprestsdk/) paketi klasöründe bir dosya içerir `cpprestsdk.targets` `\build` .

`\build`Klasör yalnızca yerel paketler değil, tüm NuGet paketleri için kullanılabilir. `\build`Klasör hedef çerçeveleri `\content` , `\lib` , ve `\tools` klasörlerine benzer. Bu, bir klasör ve klasör oluşturabileceğiniz anlamına gelir ve `\build\net40` `\build\net45` NuGet, uygun props ve hedefler dosyalarını projeye aktarır. (MSBuild hedeflerini içeri aktarmak için PowerShell betikleri kullanılması gerekli değildir.)
