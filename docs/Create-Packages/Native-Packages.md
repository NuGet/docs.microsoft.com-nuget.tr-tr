---
title: Yerel NuGet paketleri oluşturma | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Yönetilen kod yerine C++ kodunu içerir yerel NuGet paketleri oluşturma ile ilgili ayrıntılar C++ projelerinde kullanın.
keywords: NuGet yerel paketleri, NuGet C++ paketleri, C++ projeleri hedefleyen yerel kod paketleri
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ed33f906f11a80c0d033292f7de151e93b8368fd
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="creating-native-packages"></a>Yerel paketleri oluşturma

Yerel bir paket içinde C++ projeleri kullanılması izin veren, yönetilen kod yerine yerel C++ kod içerir. (Bkz [yerel C++ paketleri](../consume-packages/finding-and-choosing-packages.md#native-c-packages) Tüket bölümdeki.)

Bir C++ projesinde tüketilebilir olması için bir paket hedeflemelidir `native` framework. Olmadığından şu anda bu framework NuGet olarak ile ilişkili tüm sürüm numaralarını tüm C++ projeleri aynı değerlendirir.

> [!Note]
> Eklediğinizden emin olun *yerel* içinde `<tags>` bölümü, `.nuspec` o etiketinde arayarak paketinizi bulun diğer geliştiricilere yardımcı olmak için.

Hedefleme yerel NuGet paketlerini `native` dosyalarında sağlamak `\build`, `\content`, ve `\tools` klasörleri; `\lib` (NuGet C++ projesi başvurular doğrudan de ekleyemiyor) Bu durumda kullanılmaz. Bir paketi ayrıca hedefleri ve özellik dosyaları içerebilir `\build` NuGet paketi tüketen projelere otomatik olarak içeri aktaracak. Bu dosyalar paket kimliği ile aynı adlandırılmalıdır `.targets` ve/veya `.props` uzantıları. Örneğin, [cpprestsdk](https://nuget.org/packages/cpprestsdk/) paketi içeren bir `cpprestsdk.targets` dosyasını kendi `\build` klasör.

`\build` Klasörü tüm NuGet paketleri ve yalnızca yerel paketleri için kullanılabilir. `\build` Klasörü hedef çerçeveyi tıpkı dikkate alır `\content`, `\lib`, ve `\tools` klasörler. Oluşturabileceğiniz yani bir `\build\net40` klasör ve `\build\net45` klasörü ve NuGet içeri aktarır uygun özellik ve hedefleri dosyaları projeye. (MSBuild hedefleri almak için PowerShell komut dosyası kullanımı gerekli değildir.)
