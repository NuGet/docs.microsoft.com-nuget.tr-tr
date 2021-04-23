---
title: NuGet Uninstall-Package PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Uninstall-Package PowerShell komutuna yönelik başvuru.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 371e95c341efbce1c4a15facefc15cd51b266141
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901791"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Visual Studio 'da Paket Yöneticisi konsolu)

*Bu konuda, Windows üzerinde Visual Studio 'da [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içindeki komut açıklanmaktadır. Genel PowerShell Uninstall-Package komutu için bkz. [PowerShell PackageManagement başvurusu](/powershell/module/packagemanagement).*

, İsteğe bağlı olarak bağımlılıklarını kaldırarak bir projeden paket kaldırır. Diğer paketler bu pakete bağımlıysa, – zorlama seçeneği belirtilmediği takdirde komut başarısız olur.

## <a name="syntax"></a>Syntax

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Diğer paketler bu pakete bağımlıysa, – zorlama seçeneği belirtilmediği takdirde komut başarısız olur.

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Id | Istenir Kaldırılacak paketin tanımlayıcısı. -ID anahtarı isteğe bağlıdır. |
| Sürüm | Kaldırılacak paketin sürümü, şu anda yüklü olan sürüme varsayılan olarak ayarlanıyor. |
| RemoveDependencies | Paketi ve kullanılmayan bağımlılıklarını kaldırın. Diğer bir deyişle, herhangi bir bağımlılığın kendisine bağımlı başka bir paketi varsa, bu atlanır. |
| ProjectName | Paketin kaldırılacağı proje, varsayılan proje varsayılan olarak ayarlanıyor. |
| Force | Başka paketler buna bağımlı olsa bile, bir paketi kaldırılmasına zorlar. |
| WhatIf | , Kaldırma işlemi yapılmadan komutu çalıştırırken ne olacağını gösterir. |

Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.

## <a name="common-parameters"></a>Ortak Parametreler

`Uninstall-Package` Şu [ortak PowerShell parametrelerini](/powershell/module/microsoft.powershell.core/about/about_commonparameters)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```