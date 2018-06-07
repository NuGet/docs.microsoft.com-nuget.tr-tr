---
title: NuGet Aç-PackagePage PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda Aç PackagePage PowerShell komut başvurusu.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e64a83c01a7baac330c99fe40ba52f328a2133b8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817726"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Visual Studio'da Paket Yöneticisi Konsolu)

*3.0 + kullanım dışı; yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da.*

Proje, lisans veya belirtilen paket için rapor kötüye URL'si ile varsayılan tarayıcı başlatır.

## <a name="syntax"></a>Sözdizimi

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Kimliği | İstenen paketin paket Kimliğini. Kimliği anahtarı kendisini isteğe bağlı değil. |
| Sürüm | En son sürüm varsayılan değer olarak paketin sürümü. |
| Kaynak | Seçili kaynağı aşağı açılan kaynağındaki varsayılan değer olarak paket kaynağı. |
| Lisans | Paketin lisans URL'sini tarayıcı penceresinde açar. -Lisans ne - ReportAbuse belirtilirse, tarayıcı paketin proje URL'sini açar. |
| ReportAbuse | Paketin rapor kötüye URL'si tarayıcıda açılır. -Lisans ne - ReportAbuse belirtilirse, tarayıcı paketin proje URL'sini açar. |
| Geçiş | URL'yi görüntüler; Tarayıcı açma bastırmak için - whatIf kullanın. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.

## <a name="common-parameters"></a>Ortak parametreleri

`Open-PackagePage` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```