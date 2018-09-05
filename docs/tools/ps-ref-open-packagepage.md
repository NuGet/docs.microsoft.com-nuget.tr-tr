---
title: NuGet açık-PackagePage PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolu aç PackagePage PowerShell komutunda referansı.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0325aa4ddd718a901dd6a09cdf86cae260e326ab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547174"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Visual Studio'da Paket Yöneticisi Konsolu)

*3.0 +'da kullanım dışı; yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da.*

Proje, lisans veya rapor Uygunsuz kullanım bildirme URL'si belirtilen paket için varsayılan tarayıcıda başlatır.

## <a name="syntax"></a>Sözdizimi

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Kimliği | İstenen paketin paket kimliği. Kimliği anahtarın kendisinde, isteğe bağlıdır. |
| Sürüm | En son sürüme varsayarak paketinin sürümü. |
| Kaynak | Aşağı açılan kaynakta seçilen kaynak varsayarak paketinin kaynağı. |
| Lisans | Paketin lisans URL'si için bir tarayıcı açar. -Lisans ne - ReportAbuse belirtilirse, tarayıcı paketin proje URL'sini açar. |
| ReportAbuse | Paketin rapor Uygunsuz kullanım bildirme URL'si için bir tarayıcı açar. -Lisans ne - ReportAbuse belirtilirse, tarayıcı paketin proje URL'sini açar. |
| Geçiş | URL'yi görüntüler. -WhatIf ile tarayıcıyı açmalarını engellemek için kullanın. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.

## <a name="common-parameters"></a>Ortak parametreleri

`Open-PackagePage` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntılı, WarningAction ve WarningVariable.

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