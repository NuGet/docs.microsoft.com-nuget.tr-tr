---
title: İçinde NuGet paketini önbelleğe alma yönetme | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Farklı NuGet paketi yönetmek nasıl bir makinede mevcut yüklerken veya paketleri geri kullanılan önbelleğe alır.
keywords: NuGet paket önbellek, paketi önbelleğe alma, NuGet önbellekleri, önbellekler, NuGet yerel önbelleği, genel NuGet önbelleği, önbellek temizleme NuGet Yereller komutu yönetme
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 09b3560d67ff8a38677dd1e27d85cdf234495aae
ms.sourcegitcommit: 718e6cb88e45fa07c85d653f216bf92eaaf81625
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/23/2018
---
# <a name="managing-the-nuget-cache"></a>NuGet önbelleği yönetme

NuGet birkaç yerel önbellekleri zaten bilgisayarda olan paketlerin yüklenmesini önlemek için çevrimdışı destek sağlamak için ve yönetir. NuGet otomatik olarak geri yüklerken veya bir ağ bağlantısı olmadan paketler yeniden önbelleğe döner.

Önbellek konumlarının kullanılabilir kullanarak [Yereller komutu](../tools/cli-ref-locals.md):

```cli
nuget locals all -list
```

Tipik çıkış aşağıdaki gibidir:

```output
http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder
```

Paket yükleme sorunlarla veya aksi takdirde uzaktan galerisinden, kullanım paketleri yüklüyorsanız sağlamak istiyorsanız `locals -clear` seçeneği:

```cli
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

Önbellek yönetme şu anda yalnızca NuGet komut satırı ve Visual Studio içinde değil veya Paket Yöneticisi konsolu aracılığıyla desteklendiğini unutmayın. Ayrıca, 2.x önbelleğini yönetme NuGet 3.6 ve sonraki sürümlerinde desteklenmiyor.

Kullanırken aşağıdaki hatalar oluşabilir `nuget locals`:

- **Yerel kaynaklar temizleme başarısız oldu: bir veya daha fazla dosya silinemiyor**
- **Dizini boş değil**

Bunlar, önbellek ya da bir dosya silme iznine sahip değil veya daha fazla dosya önbelleğinde dosyaları kaldırılabilmesi için önce hangi kapatılmalıdır başka bir işlem tarafından kullanılıyor gösterir.
