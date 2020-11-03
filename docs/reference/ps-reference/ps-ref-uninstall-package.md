---
title: NuGet Uninstall-Package PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Uninstall-Package PowerShell komutuna yönelik başvuru.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: d164176355e32e5bbe0a017fc2b291cbc9ef326a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237133"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Visual Studio 'da Paket Yöneticisi konsolu)

*Bu konuda, Windows üzerinde Visual Studio 'da [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içindeki komut açıklanmaktadır. Genel PowerShell Uninstall-Package komutu için bkz. [PowerShell PackageManagement başvurusu](/powershell/module/packagemanagement/?view=powershell-6).*

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