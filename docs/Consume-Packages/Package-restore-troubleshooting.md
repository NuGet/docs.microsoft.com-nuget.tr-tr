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
ms.openlocfilehash: 374e385ecd9b9bcd71b1c61914ea03a072a5f182
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a>Visual Studio'da paket geri yükleme hatalarını giderme

> [!Note]
> Bu sayfa, bunları çözmek için Visual Studio ve adımları paketleri geri yüklenirken ortak hataları ele alınmaktadır. Nasıl yapılır konuları için paketlerini geri yüklemek için bkz: [paket geri yüklemesi](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).

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

![NuGet paket geri yüklemesi aracı/seçeneklerinde etkinleştir](../Consume-Packages/media/restore-01-autorestoreoptions.png)
