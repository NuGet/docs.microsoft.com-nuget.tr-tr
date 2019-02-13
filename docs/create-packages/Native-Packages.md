---
title: Yerel NuGet paketleri oluşturma
description: Yönetilen kod yerine C++ kodu içeren yerel NuGet paketleri oluşturma hakkında bilgi edinmek, C++ projelerinde kullanın.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e0ec5323f7be53bef6637ad69540a66abbf22711
ms.sourcegitcommit: d5a35a097e6b461ae791d9f66b3a85d5219d7305
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56145585"
---
# <a name="creating-native-packages"></a>Yerel paketler oluşturma

Yerel Paket kullanılan C++ içinde (veya benzer) izin veren Yönetilen derlemeler yerine yerel ikili dosyaları içeren projeleri. (Bkz [yerel C++ paketleri](../consume-packages/finding-and-choosing-packages.md#native-c-packages) kullanma bölümünde.)

Bir C++ projesinde kullanılabilir olması için bir paket hedeflemelidir `native` framework. Olmadığından şu anda bu çerçeve olarak NuGet ile ilişkili herhangi bir sürüm numaraları tüm C++ projeleri aynı değerlendirir.

> [!Note]
> Eklediğinizden emin olun *yerel* içinde `<tags>` bölümünü, `.nuspec` paketiniz, etiketinde arayarak bulun diğer geliştiricilerin yardımcı olmak için.

Hedefleyen yerel NuGet paketlerini `native` ardından dosyalarında sağlayın `\build`, `\content`, ve `\tools` klasörleri; `\lib` (NuGet C++ projesi başvuruları doğrudan de ekleyemiyor) Bu durumda kullanılmaz. Bir paket içinde hedeflerini ve özellik dosyalarını da içerebilir `\build` NuGet paketi kullanma projelere otomatik olarak içeri aktaracak. Bu dosyalar paket kimliği ile aynı adlandırılmalıdır `.targets` ve/veya `.props` uzantıları. Örneğin, [cpprestsdk](https://nuget.org/packages/cpprestsdk/) paketi içeren bir `cpprestsdk.targets` dosyası kendi `\build` klasör.

`\build` Klasörü tüm NuGet paketlerini ve yalnızca yerel paketleri için kullanılabilir. `\build` Klasörü hedef çerçeveleri gibi uyar `\content`, `\lib`, ve `\tools` klasörleri. Bu oluşturabileceğiniz anlamına gelir. bir `\build\net40` klasör ve bir `\build\net45` klasörü ve NuGet içeri aktarır uygun özellikler ve hedefler dosyaları projeye. (MSBuild hedefleri içeri aktarmak için PowerShell komut dosyası kullanımı gerekli değildir.)
