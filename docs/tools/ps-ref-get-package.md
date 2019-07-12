---
title: NuGet Get-Package PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolu Get-Package PowerShell komutunda referansı.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d0d25cb6e21f6d0d42389e08340b6f1e1baf8a64
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842512"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Visual Studio'da Paket Yöneticisi Konsolu)

*Bu konu içindeki komut açıklar [Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da. Genel PowerShell Get-Package komutu için bkz: [PowerShell PackageManagement başvuru](/powershell/module/packagemanagement/?view=powershell-6).*

Yerel depoda yüklü paketler listesini alır, - ListAvailable anahtarla kullanıldığında bir paket kaynağından paketleri listeler veya güncelleştirme anahtarıyla birlikte kullanıldığında kullanılabilir güncelleştirmeleri listeler.

## <a name="syntax"></a>Sözdizimi

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

Parametre olmadan `Get-Package` varsayılan projede yüklü paketler listesini görüntüler.

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Source | Paket URL'si veya klasör yolu. Yerel klasör yol mutlak veya göreli geçerli klasörde olabilir. Atlanırsa, `Get-Package` seçili paket kaynağı arar. -ListAvailable ile nuget.org varsayılan olarak kullanıldığında. |
| ListAvailable | Nuget.org için varsayılan bir paket kaynağından paketleri listeler. -PageSize ve/veya - ilk belirtilmediği sürece varsayılan olarak 50 paketler gösterilmektedir. |
| Güncelleştirmeler | Paket kaynağından bir güncelleştirmenin kullanılabilir olduğu paketleri listeler. |
| ProjectName | Yüklü paketleri alınmaya başlanacağı proje. Atlanırsa, tüm çözüm için projeleri döndürür yüklü. |
| Filtrele | Paket kimliği, açıklama ve etiket uygulayarak paketlerin listesini sınırlamak için kullanılan bir filtre dizesi. |
| ilk | Listeye başlangıcından itibaren döndürülecek paket sayısı. 50'ye belirtilmezse, varsayılan olarak. |
| Atla | İlk atlar &lt;int&gt; görüntülenen listeden paketleri.  |
| AllVersions | Tüm kullanılabilir sürümlerin her paketin yerine yalnızca en son sürümünü görüntüler. |
| IncludePrerelease | Yayın öncesi paketleri sonuçları içerir. |
| PageSize | *(3.0 +)*  - İle ListAvailable (gerekli), devam etmek için bir istem yapmadan önce listelemek için paket sayısı kullanıldığında. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.

## <a name="common-parameters"></a>Ortak parametreleri

`Get-Package` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): Hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, ayrıntılı PipelineVariable, WarningAction ve WarningVariable.

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
