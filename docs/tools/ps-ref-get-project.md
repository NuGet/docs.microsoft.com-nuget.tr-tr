---
title: NuGet Get-proje PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolu GetProject PowerShell komutunda referansı.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 2ceb1557eafd213c148d3ab870925ef5bbbee145
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842276"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Visual Studio'da Paket Yöneticisi Konsolu)

*Yalnızca içinde kullanılabilir [Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da.*

Varsayılan veya belirtilen proje hakkında bilgileri görüntüler. `Get-Project` özellikle bir grup projesi için Visual Studio DTE (geliştirme araçları ortamı) nesnesi döndürür.

## <a name="syntax"></a>Sözdizimi

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Ad | Görüntülenecek, proje, Paket Yöneticisi Konsolu'nda seçili varsayılan proje varsayarak belirtir. Ad anahtarı, kendisi isteğe bağlı. |
| Tümü | Çözümde her proje için bilgileri görüntüler; projelerin sırası belirleyici değildir. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.

## <a name="common-parameters"></a>Ortak parametreleri

`Get-Project` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): Hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, ayrıntılı PipelineVariable, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```