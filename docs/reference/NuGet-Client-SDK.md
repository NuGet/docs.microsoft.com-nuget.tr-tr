---
title: NuGet istemci SDK'sı
description: Geliştirilmekte olan ve henüz belgelenmiş API'si, ancak örnekler Dave Glick'ın blogunda kullanılabilir.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 8f96bf289e8121fd25262fb95c2f36dfc89045c5
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911042"
---
# <a name="nuget-client-sdk"></a>NuGet istemci SDK'sı

> [!Note]
> İle karıştırılmamalıdır [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)

*NuGet istemci SDK'sı* .NET kitaplıkları etrafında ortalanmış bir grup başvurduğu [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), ve [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol). Bu paketler önceki değiştirin [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) kitaplığı.

Size en kısa sürede belgelemeye kararlı bir yüzey alanı olması çalışıyoruz.

## <a name="source-code"></a>Kaynak kodu

Kaynak kodu Github'da projede yayımlanan [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).

## <a name="third-party-documentation"></a>Üçüncü taraf belgeleri

Örnekler ve belgeler için bazı API 2016 yayımlanan Dave Glick tarafından aşağıdaki blog dizisini bulabilirsiniz:

- [1. Bölüm NuGet v3 kitaplıkları keşfetme: Giriş ve kavramları](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [2. Bölüm NuGet v3 kitaplıkları keşfetme: Paketlerini arama](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Bölüm 3 NuGet v3 kitaplıkları keşfetme: Paketleri yükleme](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Bu blog gönderileri, kısa süre sonra yazılmış **3.4.3** istemci SDK paketleri kullanıma sunulan NuGet sürümü.
> Paketlerin daha yeni sürümlerini blog gönderilerini bilgileri ile uyumlu olmayabilir.

Martin Björkström burada verilen NuGet paketlerini yüklemek için NuGet istemci SDK'sını kullanarak farklı bir yaklaşım tanıtan bir izleme blog gönderisi Dave Glick'ın blog serisine yaptınız:

- [NuGet v3 kitaplıkları hakkında yeniden değerlendirme](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
