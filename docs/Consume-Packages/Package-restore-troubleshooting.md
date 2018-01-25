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
# <a name="troubleshooting-package-restore-errors-in-visual-studio"></a><span data-ttu-id="55938-104">Visual Studio'da paket geri yükleme hatalarını giderme</span><span class="sxs-lookup"><span data-stu-id="55938-104">Troubleshooting package restore errors in Visual Studio</span></span>

> [!Note]
> <span data-ttu-id="55938-105">Bu sayfa, bunları çözmek için Visual Studio ve adımları paketleri geri yüklenirken ortak hataları ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="55938-105">This page focuses on common errors when restoring packages in Visual Studio and steps to resolve them.</span></span> <span data-ttu-id="55938-106">Nasıl yapılır konuları için paketlerini geri yüklemek için bkz: [paket geri yüklemesi](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="55938-106">For how-to restore packages, see [Package restore](../Consume-Packages/Package-Restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="55938-107">Varsayılan olarak, Visual Studio Proje otomatik olarak oluşturma projede başvurulan NuGet paketleri geri yükler.</span><span class="sxs-lookup"><span data-stu-id="55938-107">By default, building a project in Visual Studio automatically restores NuGet packages referenced in the project.</span></span> <span data-ttu-id="55938-108">Bununla birlikte, paket geri yüklemesi de devre dışı bırakılırsa derlemeler başarısız olur **Araçlar > Seçenekler > NuGet Paket Yöneticisi > paketi geri yüklemesi** ayarları ve gerekli paketleri bilgisayarınızda kullanılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="55938-108">However, builds will fail if package restore is disabled in the **Tools > Options > NuGet Package Manager > Package Restore** settings and the necessary packages are not available on your computer.</span></span> <span data-ttu-id="55938-109">Bu durumlarda, aşağıdaki hatalar görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="55938-109">In these cases you may see the following errors:</span></span>

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

<span data-ttu-id="55938-110">Paket geri yüklemesi etkinleştirmek için açın **Araçlar > Seçenekler > NuGet Paket Yöneticisi** ve ilgili seçenekleri seçin **Nuget'in eksik paketleri indirmesine izin ver** ve **otomatik olarak eksik olup olmadığını denetleyin Visual Studio'da derleme sırasında paketleri**:</span><span class="sxs-lookup"><span data-stu-id="55938-110">To enable package restore, open **Tools > Options > NuGet Package Manager** and select the options for **Allow NuGet to download missing packages** and **Automatically check for missing packages during build in Visual Studio**:</span></span>

![NuGet paket geri yüklemesi aracı/seçeneklerinde etkinleştir](../Consume-Packages/media/restore-01-autorestoreoptions.png)
