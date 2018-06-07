---
title: NuGet Get-proje PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda GetProject PowerShell komut başvurusu.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: afdf9f762bbd34531f9d9093238a2fed27e3f4d3
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817762"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Visual Studio'da Paket Yöneticisi Konsolu)

*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da.*

Varsayılan ya da belirtilen proje hakkındaki bilgileri görüntüler. `Get-Project` özellikle bir tfs'deki projesi için Visual Studio DTE (geliştirme araçları ortamı) nesnesi döndürür.

## <a name="syntax"></a>Sözdizimi

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Ad | Paket Yöneticisi Konsolu'nda seçili olan varsayılan projeyi varsayarak görüntülemek için projeyi belirtir. -Name anahtarı kendisini isteğe bağlı değil. |
| Tümü | Çözümdeki her projeye ilgili bilgileri görüntüler; projelerin sırası belirleyici değildir. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.

## <a name="common-parameters"></a>Ortak parametreleri

`Get-Project` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```