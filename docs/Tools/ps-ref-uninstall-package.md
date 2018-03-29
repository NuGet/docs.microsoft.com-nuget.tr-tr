---
title: NuGet kaldırma paketi PowerShell başvurusu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda Uninstall-Package PowerShell komut başvurusu.
keywords: NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu, Uninstall-Package
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: b53a36a6456522aa0d9d0d7cdf412de464ba9e08
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Kaldırma paket (Visual Studio'da Paket Yöneticisi Konsolu)

*Bu konu içindeki komut açıklar [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da. Genel PowerShell Uninstall-Package komutu için bkz: [PowerShell PackageManagement başvuru](/powershell/module/packagemanagement/?view=powershell-6).*

Bir paket bağımlılıklarını isteğe bağlı olarak kaldırarak bir projeden kaldırır. Diğer paketler bu pakete bağlıysa, komut sürece başarısız olur – Force seçeneği.

## <a name="syntax"></a>Sözdizimi

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Diğer paketler bu pakete bağlıysa, komut sürece başarısız olur – Force seçeneği.

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Kimliği | (Gerekli) Kaldırılacak paketin tanımlayıcısı. Kimliği anahtarı kendisini isteğe bağlı değil. |
| Sürüm | Kaldırmak için paketin sürümü şu anda yüklü olan sürümle varsayılan olarak ayarlanıyor. |
| RemoveDependencies | Paketi ve kullanılmayan bağımlılıklarını kaldırın. Diğer bir deyişle, herhangi bir bağımlılığı bağımlı başka bir paket varsa atlanır. |
| ProjectName | Proje, varsayılan proje için varsayılan değer olarak bu paketi kaldırmak. |
| Force | Diğer paket bağımlı olsa bile kaldırılması için bir paket zorlar. |
| WhatIf | Kaldırma işlemini gerçekleştirmeden çalıştırırken ne olacağını gösterir. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.

## <a name="common-parameters"></a>Ortak parametreleri

`Uninstall-Package` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
