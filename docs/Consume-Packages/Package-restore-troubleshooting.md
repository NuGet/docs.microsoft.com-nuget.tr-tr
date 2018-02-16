---
title: "Geri yükleme Visual Studio'da NuGet paketi sorunlarını giderme | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Visual Studio ve bunları gidermek nasıl hatalar geri yükleme ortak NuGet açıklaması."
keywords: "NuGet paket geri yüklemesi, geri yükleme paketleri, sorun giderme, sorun giderme"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0993e2585452e3c64da28d14bb1bbe1bea27768
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/14/2018
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>Visual Studio'da paket geri yükleme hatalarını giderme

> [!Note]
> Bu sayfa, bunları çözmek için Visual Studio ve adımları paketleri geri yüklenirken ortak hataları ele alınmaktadır. Nasıl yapılır konuları için paketlerini geri yüklemek için bkz: [paket geri yüklemesi](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

Varsayılan olarak, Visual Studio Proje otomatik olarak oluşturma projede başvurulan NuGet paketleri geri yükler. Bununla birlikte, paket geri yüklemesi de devre dışı bırakılırsa derlemeler başarısız olur **Araçlar > Seçenekler > NuGet Paket Yöneticisi > paketi geri yüklemesi** ayarları ve gerekli paketleri bilgisayarınızda kullanılabilir değildir. Bu durumlarda, aşağıdaki hatalar görebilirsiniz:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name} 
```

Paket geri yüklemesi etkinleştirmek için açın **Araçlar > Seçenekler > NuGet Paket Yöneticisi** ve ilgili seçenekleri seçin **Nuget'in eksik paketleri indirmesine izin ver** ve **otomatik olarak eksik olup olmadığını denetleyin Visual Studio'da derleme sırasında paketleri**:

![NuGet paket geri yüklemesi aracı/seçeneklerinde etkinleştir](../consume-packages/media/restore-01-autorestoreoptions.png)
