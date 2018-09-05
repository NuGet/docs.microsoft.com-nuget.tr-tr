---
title: Yerel NuGet paketleri oluşturma
description: Yönetilen kod yerine C++ kodu içeren yerel NuGet paketleri oluşturma hakkında bilgi edinmek, C++ projelerinde kullanın.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: f054a1cae7328d3e910d11ac1bfc5f98505e5879
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546539"
---
# <a name="creating-native-packages"></a>Yerel paketler oluşturma

Yerel Paket C++ projesi içinde kullanılacak veren yönetilen kod yerine yerel C++ kodunu içerir. (Bkz [yerel C++ paketleri](../consume-packages/finding-and-choosing-packages.md#native-c-packages) kullanma bölümünde.)

Bir C++ projesinde kullanılabilir olması için bir paket hedeflemelidir `native` framework. Olmadığından şu anda bu çerçeve olarak NuGet ile ilişkili herhangi bir sürüm numaraları tüm C++ projeleri aynı değerlendirir.

> [!Note]
> Eklediğinizden emin olun *yerel* içinde `<tags>` bölümünü, `.nuspec` paketiniz, etiketinde arayarak bulun diğer geliştiricilerin yardımcı olmak için.

Hedefleyen yerel NuGet paketlerini `native` ardından dosyalarında sağlayın `\build`, `\content`, ve `\tools` klasörleri; `\lib` (NuGet C++ projesi başvuruları doğrudan de ekleyemiyor) Bu durumda kullanılmaz. Bir paket içinde hedeflerini ve özellik dosyalarını da içerebilir `\build` NuGet paketi kullanma projelere otomatik olarak içeri aktaracak. Bu dosyalar paket kimliği ile aynı adlandırılmalıdır `.targets` ve/veya `.props` uzantıları. Örneğin, [cpprestsdk](https://nuget.org/packages/cpprestsdk/) paketi içeren bir `cpprestsdk.targets` dosyası kendi `\build` klasör.

`\build` Klasörü tüm NuGet paketlerini ve yalnızca yerel paketleri için kullanılabilir. `\build` Klasörü hedef çerçeveleri gibi uyar `\content`, `\lib`, ve `\tools` klasörleri. Bu oluşturabileceğiniz anlamına gelir. bir `\build\net40` klasör ve bir `\build\net45` klasörü ve NuGet içeri aktarır uygun özellikler ve hedefler dosyaları projeye. (MSBuild hedefleri içeri aktarmak için PowerShell komut dosyası kullanımı gerekli değildir.)
