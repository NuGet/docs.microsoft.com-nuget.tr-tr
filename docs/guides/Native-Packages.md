---
title: Yerel NuGet paketleri oluşturma
description: Projelerde kullanılmak üzere, yönetilen kod yerine kodu C++ Içeren yerel NuGet paketleri oluşturma hakkında ayrıntılar. C++
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e0ec5323f7be53bef6637ad69540a66abbf22711
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520599"
---
# <a name="creating-native-packages"></a>Yerel paketler oluşturma

Yerel bir paket yönetilen derlemeler yerine yerel ikili dosyalar içerir ve bunun C++ (veya benzer) projelerde kullanılmasına izin verir. (Tüketme bölümünde [yerel C++ paketlere](../consume-packages/finding-and-choosing-packages.md#native-c-packages) bakın.)

Bir C++ projede tüketilebilir olması için, bir paketin `native` çerçeveyi hedeflemesi gerekir. Mevcut olduğunda, NuGet tüm C++ projelere aynı şekilde davrandığı için bu Framework ile ilişkili herhangi bir sürüm numarası yoktur.

> [!Note]
> Diğer geliştiricilerin bu etiketi arayarak paketinizi bulmasını `<tags>` sağlamak `.nuspec` için, ' ın bölümüne yerel ' i eklediğinizden emin olun.

`native` Daha sonra `\build`, `\content`ve klasörlerindedosyalarısağlayanyerelNuGetpaketleri;`\tools` Bu durumda kullanılmıyor (NuGet bir C++ projeye doğrudan başvuru ekleyemez). `\lib` Bir paket Ayrıca, NuGet `\build` 'in paketi kullanan projelere otomatik olarak aktarılacağı hedefleri ve props dosyalarını da içerebilir. Bu dosyalar, `.targets` ve/veya `.props` uzantılarına sahip paket kimliğiyle aynı ada sahip olmalıdır. Örneğin, [cpprestsdk](https://nuget.org/packages/cpprestsdk/) paketi `cpprestsdk.targets` `\build` klasöründe bir dosya içerir.

`\build` Klasör yalnızca yerel paketler değil, tüm NuGet paketleri için kullanılabilir. Klasör hedef çerçeveleri `\content`, `\lib`, ve`\tools` klasörlerine benzer. `\build` Bu, bir `\build\net40` klasör `\build\net45` ve klasör oluşturabileceğiniz anlamına gelir ve NuGet, uygun props ve hedefler dosyalarını projeye aktarır. (MSBuild hedeflerini içeri aktarmak için PowerShell betikleri kullanılması gerekli değildir.)
