---
title: NuGet bul-Package PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Find-Package PowerShell komutu için başvuru.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4118b5a38f80a2300b3945738315d56bda096f9a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384639"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Visual Studio'da Paket Yöneticisi Konsolu)

*Sürüm 3.0 +; Bu konuda, Windows üzerinde Visual Studio 'da [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içindeki komut açıklanmaktadır. Genel PowerShell bul-Package komutu için bkz. [PowerShell PackageManagement başvurusu](/powershell/module/packagemanagement/?view=powershell-6).*

Belirtilen KIMLIĞE veya anahtar sözcüklere sahip uzak paket kümesini paket kaynağından alır.

## <a name="syntax"></a>Sözdizimi

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Kimlik &lt;anahtar sözcükleri&gt; | Istenir Paket kaynağı aranırken kullanılacak anahtar sözcükler. Yalnızca paket KIMLIĞI anahtar sözcüklerle eşleşen paketleri döndürmek için-ExactMatch kullanın. Hiçbir anahtar sözcük verilmezse, `Find-Package` indirmeleri veya Ilk olarak belirtilen sayıyı, en çok kullanılan 20 paketin bir listesini döndürür. Kimliğin isteğe bağlı olduğunu ve bir op olmadığını unutmayın. |
| Kaynak | Aranacak paket kaynağının URL veya klasör yolu. Yerel klasör yolları mutlak veya geçerli klasöre göreli olabilir. Atlanırsa, `Find-Package` Şu anda seçili olan paket kaynağını arar. |
| AllVersions | Her bir paketin yalnızca en son sürümü yerine tüm kullanılabilir sürümlerini görüntüler. |
| Birinci | Listenin başından döndürülecek paket sayısı; Varsayılan değer 20 ' dir. |
| Atla | Görünen listeden ilk &lt;int&gt; paketlerini atlar.  |
| Includeönsürümü | Sonuçlarda yayın öncesi paketleri içerir. |
| ExactMatch | Büyük/küçük harfe duyarlı paket KIMLIĞI olarak&gt; &lt;anahtar sözcüklerini kullanmak için belirtilir. |
| StartWith | Paket KIMLIĞI &lt;anahtar sözcüklerle başlayan paketleri döndürür&gt;. |

Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.

## <a name="common-parameters"></a>Ortak Parametreler

`Find-Package`, şu [ortak PowerShell parametrelerini](https://go.microsoft.com/fwlink/?LinkID=113216)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.

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
