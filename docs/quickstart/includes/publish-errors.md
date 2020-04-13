---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496004"
---
Komuttaki `push` hatalar genellikle sorunu gösterir. Örneğin, projenizdeki sürüm numarasını güncelleştirmeyi unutmuş olabilirsiniz ve bu nedenle zaten var olan bir paketi yayımlamaya çalışıyorsunuz.

Ayrıca, ana bilgisayarda zaten var olan bir tanımlayıcıyı kullanarak bir paketi yayımlamaya çalışırken de hatalar görürsünüz. Adı "AppLogger", örneğin, zaten var. Böyle bir durumda, `push` komut aşağıdaki hatayı verir:

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

Yeni oluşturduğunuz geçerli bir API anahtarı kullanıyorsanız, bu ileti hatanın "izin" kısmından tamamen açık olmayan bir adlandırma çakışması gösterir. Paket tanımlayıcısını değiştirin, projeyi yeniden oluşturun, `.nupkg` dosyayı yeniden `push` oluşturun ve komutu yeniden deneyin.