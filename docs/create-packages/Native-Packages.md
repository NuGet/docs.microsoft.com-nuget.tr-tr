---
title: Yerel NuGet paketleri oluşturma
description: Yönetilen kod yerine C++ kodunu içerir yerel NuGet paketleri oluşturma ile ilgili ayrıntılar C++ projelerinde kullanın.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 086084bdfae5eace0b0a6aab17140a1fa48ae977
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817066"
---
# <a name="creating-native-packages"></a>Yerel paketleri oluşturma

Yerel bir paket içinde C++ projeleri kullanılması izin veren, yönetilen kod yerine yerel C++ kod içerir. (Bkz [yerel C++ paketleri](../consume-packages/finding-and-choosing-packages.md#native-c-packages) Tüket bölümdeki.)

Bir C++ projesinde tüketilebilir olması için bir paket hedeflemelidir `native` framework. Olmadığından şu anda bu framework NuGet olarak ile ilişkili tüm sürüm numaralarını tüm C++ projeleri aynı değerlendirir.

> [!Note]
> Eklediğinizden emin olun *yerel* içinde `<tags>` bölümü, `.nuspec` o etiketinde arayarak paketinizi bulun diğer geliştiricilere yardımcı olmak için.

Hedefleme yerel NuGet paketlerini `native` dosyalarında sağlamak `\build`, `\content`, ve `\tools` klasörleri; `\lib` (NuGet C++ projesi başvurular doğrudan de ekleyemiyor) Bu durumda kullanılmaz. Bir paketi ayrıca hedefleri ve özellik dosyaları içerebilir `\build` NuGet paketi tüketen projelere otomatik olarak içeri aktaracak. Bu dosyalar paket kimliği ile aynı adlandırılmalıdır `.targets` ve/veya `.props` uzantıları. Örneğin, [cpprestsdk](https://nuget.org/packages/cpprestsdk/) paketi içeren bir `cpprestsdk.targets` dosyasını kendi `\build` klasör.

`\build` Klasörü tüm NuGet paketleri ve yalnızca yerel paketleri için kullanılabilir. `\build` Klasörü hedef çerçeveyi tıpkı dikkate alır `\content`, `\lib`, ve `\tools` klasörler. Oluşturabileceğiniz yani bir `\build\net40` klasör ve `\build\net45` klasörü ve NuGet içeri aktarır uygun özellik ve hedefleri dosyaları projeye. (MSBuild hedefleri almak için PowerShell komut dosyası kullanımı gerekli değildir.)
