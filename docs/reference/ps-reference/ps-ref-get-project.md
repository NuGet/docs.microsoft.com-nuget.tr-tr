---
title: NuGet Get-Project PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki GetProject PowerShell komutu için başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 3343952535c2d3c822f5cac24cb30c8f5bfa5be3
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384626"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Visual Studio'da Paket Yöneticisi Konsolu)

*Yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*

Varsayılan veya belirtilen proje hakkındaki bilgileri görüntüler. `Get-Project` özel olarak, projenin Visual Studio DTE (geliştirme araçları ortamı) nesnesine bir başvuru döndürür.

## <a name="syntax"></a>Sözdizimi

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Name | Görüntülenecek projeyi, varsayılan projenin Paket Yöneticisi konsolunda seçili olduğunu belirtir. -Name anahtarının kendisi isteğe bağlıdır. |
| Tümü | Çözümdeki her proje için bilgi görüntüler; projelerin sırası belirleyici değildir. |

Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.

## <a name="common-parameters"></a>Ortak Parametreler

`Get-Project`, şu [ortak PowerShell parametrelerini](https://go.microsoft.com/fwlink/?LinkID=113216)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```