---
title: "İçinde NuGet paketini önbelleğe alma yönetme | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/26/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3932217d-780d-4bd1-ad15-767acd3e8870
description: "Farklı NuGet paketi yönetmek nasıl bir makinede mevcut yüklerken veya paketleri geri kullanılan önbelleğe alır."
keywords: "NuGet paket önbellek, paketi önbelleğe alma, NuGet önbellekleri, önbellekler, NuGet yerel önbelleği, genel NuGet önbelleği, önbellek temizleme NuGet Yereller komutu yönetme"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6e76c219ba420eb285af20e67b26dcdceebb6bab
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="managing-the-nuget-cache"></a>NuGet önbelleği yönetme

NuGet birkaç yerel önbellekleri zaten bilgisayarda olan paketlerin yüklenmesini önlemek için çevrimdışı destek sağlamak için ve yönetir. NuGet 2.8 + otomatik olarak geri yüklerken veya bir ağ bağlantısı olmadan paketler yeniden önbelleğe döner.

Önbellek konumlarının kullanılabilir kullanarak [Yereller komutu](../tools/cli-ref-locals.md):

```
nuget locals all -list
```

Tipik çıkış aşağıdaki gibidir:

    http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
    packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
    global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
    temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder

Paket yükleme sorunlarla veya aksi takdirde uzaktan galerisinden, kullanım paketleri yüklüyorsanız sağlamak istiyorsanız `locals -clear` seçeneği:

```
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

Önbellek yönetme şu anda yalnızca NuGet komut satırı ve Visual Studio içinde değil veya Paket Yöneticisi konsolu aracılığıyla desteklendiğini unutmayın. Ayrıca, 2.x önbelleğini yönetme NuGet 3.6 ve sonraki sürümlerinde desteklenmiyor.

Kullanırken aşağıdaki hatalar oluşabilir `nuget locals`:

* **Yerel kaynaklar temizleme başarısız oldu: bir veya daha fazla dosya silinemiyor**
* **Dizini boş değil**

Bu önbellek ya da bir dosya silme iznine sahip değil veya daha fazla dosya önbelleğindeki önce olanlar kapatılmalıdır başka bir işlem tarafından kullanılıyor belirtmek dosyaları kaldırılabilir.
