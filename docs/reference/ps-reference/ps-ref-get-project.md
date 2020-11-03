---
title: NuGet Get-Project PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki GetProject PowerShell komutu için başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 6d9e1d48c8e1838f193878cab3483b1bfba7d7f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238081"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Visual Studio 'da Paket Yöneticisi konsolu)

*Yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*

Varsayılan veya belirtilen proje hakkındaki bilgileri görüntüler. `Get-Project` Özellikle, projenin Visual Studio DTE (geliştirme araçları ortamı) nesnesine bir başvuru döndürür.

## <a name="syntax"></a>Sözdizimi

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Ad | Görüntülenecek projeyi, varsayılan projenin Paket Yöneticisi konsolunda seçili olduğunu belirtir. -Name anahtarının kendisi isteğe bağlıdır. |
| Tümü | Çözümdeki her proje için bilgi görüntüler; projelerin sırası belirleyici değildir. |

Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.

## <a name="common-parameters"></a>Ortak Parametreler

`Get-Project` Şu [ortak PowerShell parametrelerini](/powershell/module/microsoft.powershell.core/about/about_commonparameters)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```