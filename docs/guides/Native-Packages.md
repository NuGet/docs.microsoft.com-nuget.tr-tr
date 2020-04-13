---
title: Yerli NuGet Paketleri Oluşturma
description: C++ projelerinde kullanılmak üzere yönetilen kod yerine C++ kodu içeren yerel NuGet paketleri oluşturma yla ilgili ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e0ec5323f7be53bef6637ad69540a66abbf22711
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "69520599"
---
# <a name="creating-native-packages"></a>Yerel paketler oluşturma

Yerel paket, yönetilen derlemeler yerine yerel ikililer içerir ve c++ (veya benzer) projelerde kullanılmasına izin verir. (Bkz. Tüket bölümündeki [Yerel C++ Paketleri.)](../consume-packages/finding-and-choosing-packages.md#native-c-packages)

Bir C++ projesinde tüketilebilir olması için, `native` bir paketin çerçeveyi hedeflemesi gerekir. NuGet tüm C++ projelerine aynı şekilde davrandığı ndan, şu anda bu çerçeveyle ilişkili herhangi bir sürüm numarası yoktur.

> [!Note]
> Diğer geliştiricilerin bu `<tags>` etikette `.nuspec` arama yaparak paketinizi bulmasına yardımcı olmak için bölümünüze *yerel* olarak eklediğinden emin olun.

Yerel NuGet paketleri `native` hedefleme sonra `\build` `\content`dosyaları `\tools` sağlamak , , , ve klasörler; `\lib` bu durumda kullanılmaz (NuGet doğrudan bir C++ projesine başvuru ekleyemez). Bir paket, NuGet'in paketi `\build` tüketen projelere otomatik olarak aktaracağı hedefler ve sahne dosyaları da içerebilir. Bu dosyalar, `.targets` ve/veya `.props` uzantılı paket kimliğiyle aynı adlandırılmış olmalıdır. Örneğin, [cpprestsdk](https://nuget.org/packages/cpprestsdk/) paketi `cpprestsdk.targets` `\build` klasöründe bir dosya içerir.

Klasör, `\build` sadece yerel paketler için değil, tüm NuGet paketleri için kullanılabilir. Klasör, `\build` `\content`hedef `\lib`çerçevelere ve `\tools` klasörlere benzer şekilde saygı duyar. Bu, bir `\build\net40` klasör ve `\build\net45` bir klasör oluşturabileceğiniz ve NuGet'in uygun sahne ve hedef dosyalarını projeye aktaracağı anlamına gelir. (MSBuild hedeflerini almak için PowerShell komut dosyalarının kullanılması gerekmez.)
