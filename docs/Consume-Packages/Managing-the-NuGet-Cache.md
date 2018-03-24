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
# <a name="managing-the-nuget-cache"></a><span data-ttu-id="9b4d6-104">NuGet önbelleği yönetme</span><span class="sxs-lookup"><span data-stu-id="9b4d6-104">Managing the NuGet cache</span></span>

<span data-ttu-id="9b4d6-105">NuGet birkaç yerel önbellekleri zaten bilgisayarda olan paketlerin yüklenmesini önlemek için çevrimdışı destek sağlamak için ve yönetir.</span><span class="sxs-lookup"><span data-stu-id="9b4d6-105">NuGet manages several local caches to avoid downloading packages that are already on the computer, and to provide offline support.</span></span> <span data-ttu-id="9b4d6-106">NuGet otomatik olarak geri yüklerken veya bir ağ bağlantısı olmadan paketler yeniden önbelleğe döner.</span><span class="sxs-lookup"><span data-stu-id="9b4d6-106">NuGet automatically falls back to the cache when installing or reinstalling packages without a network connection.</span></span>

<span data-ttu-id="9b4d6-107">Önbellek konumlarının kullanılabilir kullanarak [Yereller komutu](../tools/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="9b4d6-107">Cache locations are available using the [locals command](../tools/cli-ref-locals.md):</span></span>

```cli
nuget locals all -list
```

<span data-ttu-id="9b4d6-108">Tipik çıkış aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9b4d6-108">Typical output is as follows:</span></span>

```output
http-cache: C:\Users\user\AppData\Local\NuGet\v3-cache   #NuGet 3.x+ cache
packages-cache: C:\Users\user\AppData\Local\NuGet\Cache  #NuGet 2.x cache
global-packages: C:\Users\user\.nuget\packages\          #Global packages folder
temp: C:\Users\user\AppData\Local\Temp\NuGetScratch      #Temp folder
```

<span data-ttu-id="9b4d6-109">Paket yükleme sorunlarla veya aksi takdirde uzaktan galerisinden, kullanım paketleri yüklüyorsanız sağlamak istiyorsanız `locals -clear` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="9b4d6-109">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals -clear` option:</span></span>

```cli
nuget locals http-cache -clear        #Clear the 3.x+ cache
nuget locals packages-cache -clear    #Clear the 2.x cache
nuget locals global-packages -clear   #Clear the global packages folder
nuget locals temp -clear              #Clear the temporary cache
nuget locals all -clear               #Clear all caches
```

<span data-ttu-id="9b4d6-110">Önbellek yönetme şu anda yalnızca NuGet komut satırı ve Visual Studio içinde değil veya Paket Yöneticisi konsolu aracılığıyla desteklendiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9b4d6-110">Note that managing the cache is presently supported only from the NuGet command line, and not within Visual Studio or through the Package Manager Console.</span></span> <span data-ttu-id="9b4d6-111">Ayrıca, 2.x önbelleğini yönetme NuGet 3.6 ve sonraki sürümlerinde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="9b4d6-111">Also, managing the 2.x cache is not supported in NuGet 3.6 and later.</span></span>

<span data-ttu-id="9b4d6-112">Kullanırken aşağıdaki hatalar oluşabilir `nuget locals`:</span><span class="sxs-lookup"><span data-stu-id="9b4d6-112">The following errors can occur when using `nuget locals`:</span></span>

- <span data-ttu-id="9b4d6-113">**Yerel kaynaklar temizleme başarısız oldu: bir veya daha fazla dosya silinemiyor**</span><span class="sxs-lookup"><span data-stu-id="9b4d6-113">**Clearing local resources failed: Unable to delete one or more files**</span></span>
- <span data-ttu-id="9b4d6-114">**Dizini boş değil**</span><span class="sxs-lookup"><span data-stu-id="9b4d6-114">**The directory is not empty**</span></span>

<span data-ttu-id="9b4d6-115">Bunlar, önbellek ya da bir dosya silme iznine sahip değil veya daha fazla dosya önbelleğinde dosyaları kaldırılabilmesi için önce hangi kapatılmalıdır başka bir işlem tarafından kullanılıyor gösterir.</span><span class="sxs-lookup"><span data-stu-id="9b4d6-115">These indicate that you either do not have permission to delete files in the cache, or that one or more files in the cache are in use by another process, which must be closed before the files can be removed.</span></span>
