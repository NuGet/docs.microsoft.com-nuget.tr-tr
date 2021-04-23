---
title: NuGet Find-Package PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Find-Package PowerShell komutuna yönelik başvuru.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 263835da64340a13737b32ab54ab057cb640a080
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901765"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Visual Studio 'da Paket Yöneticisi konsolu)

*Sürüm 3.0 +; Bu konuda, Windows üzerinde Visual Studio 'da [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içindeki komut açıklanmaktadır. Genel PowerShell Find-Package komutu için bkz. [PowerShell PackageManagement başvurusu](/powershell/module/packagemanagement).*

Belirtilen KIMLIĞE veya anahtar sözcüklere sahip uzak paket kümesini paket kaynağından alır.

## <a name="syntax"></a>Sözdizimi

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Kimlik &lt; anahtar sözcükleri&gt; | Istenir Paket kaynağı aranırken kullanılacak anahtar sözcükler. Yalnızca paket KIMLIĞI anahtar sözcüklerle eşleşen paketleri döndürmek için-ExactMatch kullanın. Hiçbir anahtar sözcük verilmezse, `Find-Package` indirmelere göre ilk 20 paketin bir listesini ya da önce tarafından belirtilen sayıyı döndürür. Kimliğin isteğe bağlı olduğunu ve bir op olmadığını unutmayın. |
| Kaynak | Aranacak paket kaynağının URL veya klasör yolu. Yerel klasör yolları mutlak veya geçerli klasöre göreli olabilir. Atlanırsa, `Find-Package` Şu anda seçili olan paket kaynağını arar. |
| AllVersions | Her bir paketin yalnızca en son sürümü yerine tüm kullanılabilir sürümlerini görüntüler. |
| Birinci | Listenin başından döndürülecek paket sayısı; Varsayılan değer 20 ' dir. |
| Atla | &lt;Görüntülenmiş listedeki ilk int &gt; paketleri atlar.  |
| Includeönsürümü | Sonuçlarda yayın öncesi paketleri içerir. |
| ExactMatch | &lt;Anahtar sözcükleri, &gt; büyük/küçük harfe duyarlı BIR paket kimliği olarak kullanmak için belirtilmiştir. |
| StartWith | Paket KIMLIĞI anahtar sözcüklerle başlayan paketleri döndürür &lt; &gt; . |

Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.

## <a name="common-parameters"></a>Ortak Parametreler

`Find-Package` Şu [ortak PowerShell parametrelerini](/powershell/module/microsoft.powershell.core/about/about_commonparameters)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```