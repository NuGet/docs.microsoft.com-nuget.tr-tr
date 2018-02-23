---
title: "NuGet Get-Package PowerShell başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio'da NuGet Paket Yöneticisi konsolunda Get-Package PowerShell komut başvurusu."
keywords: "NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu, Get-Package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 01a874ce9ae59dcaeb696a45f23cc5e9f2cfa251
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/20/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Visual Studio'da Paket Yöneticisi Konsolu)

*Bu konu içindeki komut açıklar [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da. Genel PowerShell Get-Package komutu için bkz: [PowerShell PackageManagement başvuru](/powershell/module/packagemanagement/?view=powershell-6).*

Yerel depoda yüklü olan paketlerin listesini alır, - listavailable birlikte anahtarıyla birlikte kullanıldığında bir paket kaynağındaki paketleri listeler veya güncelleştirme anahtarıyla birlikte kullanıldığında kullanılabilir güncelleştirmeleri listeler.

## <a name="syntax"></a>Sözdizimi

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Hiçbir parametre `Get-Package` varsayılan projede yüklü olan paketlerin listesini görüntüler.

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Kaynak | Paket URL'si veya klasör yolu. Yerel klasör yolları mutlak veya göreli geçerli klasörde olabilir. Atlanırsa, `Get-Package` şu anda seçili paket kaynağını arar. -Listavailable ile birlikte, nuget.org varsayılanlara kullanıldığında. |
| Listavailable birlikte | Nuget.org için varsayılan değer olarak, bir paket kaynağındaki paketleri listeler. -PageSize ve/veya - ilk belirtilmediği sürece varsayılan 50 paketlerin gösterir. |
| Güncelleştirmeler | Paket kaynağındaki güncelleştirmeye sahip paketleri listeler. |
| ProjectName | Yüklü paketler alınacağı projesi. Atlanırsa, çözümün tamamı için projeleri döndürür yüklü. |
| Filtrele | Paket kimliği, açıklamada ve etiketlerde uygulayarak paket listesini daraltmak için kullanılan bir filtre dizesi. |
| ilk | Listenin başlangıcından döndürülecek paket sayısı. Belirtilmezse, 50'ye varsayılan olur. |
| Atla | İlk atlar &lt;int&gt; görüntülenen listeden paketler.  |
| AllVersions | Yalnızca en son sürümü yerine her paketin tüm kullanılabilir sürümlerini görüntüler. |
| IncludePrerelease | Sonuçlarda Önsürüm paketlerinin içerir. |
| PageSize | *(3.0 +)*  -(Gerekli) listavailable ile birlikte, devam etmek için bir istem vermeden önce listelemek için paket sayısı kullanıldığında. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.

## <a name="common-parameters"></a>Ortak parametreleri

`Get-Package` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```
