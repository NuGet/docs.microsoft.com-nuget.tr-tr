---
title: NuGet açık-PackagePage PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolu aç PackagePage PowerShell komutunda referansı.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fd738f15b461051c4e9413b3035456c687979b97
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842261"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Visual Studio'da Paket Yöneticisi Konsolu)

*3.0 +'da kullanım dışı; yalnızca içinde kullanılabilir [Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da.*

Proje, lisans veya rapor Uygunsuz kullanım bildirme URL'si belirtilen paket için varsayılan tarayıcıda başlatır.

## <a name="syntax"></a>Sözdizimi

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Id | İstenen paketin paket kimliği. Kimliği anahtarın kendisinde, isteğe bağlıdır. |
| Sürüm | En son sürüme varsayarak paketinin sürümü. |
| Source | Aşağı açılan kaynakta seçilen kaynak varsayarak paketinin kaynağı. |
| Lisans | Paketin lisans URL'si için bir tarayıcı açar. -Lisans ne - ReportAbuse belirtilirse, tarayıcı paketin proje URL'sini açar. |
| ReportAbuse | Paketin rapor Uygunsuz kullanım bildirme URL'si için bir tarayıcı açar. -Lisans ne - ReportAbuse belirtilirse, tarayıcı paketin proje URL'sini açar. |
| PassThru | URL'yi görüntüler. -WhatIf ile tarayıcıyı açmalarını engellemek için kullanın. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.

## <a name="common-parameters"></a>Ortak parametreleri

`Open-PackagePage` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): Hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, ayrıntılı PipelineVariable, WarningAction ve WarningVariable.

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