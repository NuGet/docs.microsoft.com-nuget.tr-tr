---
title: NuGet Get-Package PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Get-Package PowerShell komutuna yönelik başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 1576e3f20eba1ecdd099b1e7c23aef6b1a1a0a4f
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237237"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Visual Studio 'da Paket Yöneticisi konsolu)

*Bu konuda, Windows üzerinde Visual Studio 'da [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içindeki komut açıklanmaktadır. Genel PowerShell Get-Package komutu için bkz. [PowerShell PackageManagement başvurusu](/powershell/module/packagemanagement/?view=powershell-6).*

Yerel depoda yüklü paketlerin listesini alır,-ListAvailable anahtarıyla birlikte kullanıldığında bir paket kaynağından kullanılabilir olan paketleri listeler veya-Update anahtarıyla birlikte kullanıldığında kullanılabilir güncelleştirmeleri listeler.

## <a name="syntax"></a>Syntax

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Parametresiz, `Get-Package` varsayılan projede yüklü paketlerin listesini görüntüler.

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Kaynak | Paketin URL veya klasör yolu. Yerel klasör yolları mutlak veya geçerli klasöre göreli olabilir. Atlanırsa, `Get-Package` Şu anda seçili olan paket kaynağını arar. -ListAvailable ile kullanıldığında varsayılan olarak nuget.org olur. |
| ListAvailable | Bir paket kaynağından kullanılabilir olan paketleri listeler, varsayılan olarak nuget.org. -PageSize ve/veya-First belirtilmemişse, varsayılan 50 paket gösterir. |
| Güncelleştirmeler | Paket kaynağından kullanılabilir bir güncelleştirme olan paketleri listeler. |
| ProjectName | Yüklü paketlerin alınacağı proje. Atlanırsa, tüm çözüm için yüklü projeleri döndürür. |
| Filtre | Paket KIMLIĞINE, açıklamaya ve etiketlere uygulayarak paket listesini daraltmak için kullanılan bir filtre dizesi. |
| Birinci | Listenin başından döndürülecek paket sayısı. Belirtilmemişse, varsayılan olarak 50 ' dir. |
| Atla | &lt;Görüntülenmiş listedeki ilk int &gt; paketleri atlar.  |
| AllVersions | Her bir paketin yalnızca en son sürümü yerine tüm kullanılabilir sürümlerini görüntüler. |
| Includeönsürümü | Sonuçlarda yayın öncesi paketleri içerir. |
| PageSize | *(3.0 +)* -ListAvailable (zorunlu) ile kullanıldığında, devam etmek için bir istem vermeden önce listeye eklenecek paket sayısı. |

Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.

## <a name="common-parameters"></a>Ortak Parametreler

`Get-Package` Şu [ortak PowerShell parametrelerini](/powershell/module/microsoft.powershell.core/about/about_commonparameters)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.

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