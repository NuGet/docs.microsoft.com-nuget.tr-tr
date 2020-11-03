---
title: NuGet Open-PackagePage PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Open-PackagePage PowerShell komutuna yönelik başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ba90e09c017ec66d73c35a60025474bc77cf65a7
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238068"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Visual Studio 'da Paket Yöneticisi konsolu)

*3.0 + ' da kullanımdan kaldırılmıştır; yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*

Belirtilen paket için proje, lisans veya uygunsuz kullanım URL 'SI ile varsayılan tarayıcıyı başlatır.

## <a name="syntax"></a>Sözdizimi

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Id | İstenen paketin paket KIMLIĞI. -ID anahtarı isteğe bağlıdır. |
| Sürüm | Paketin sürümü, en son sürümü varsayılan olarak sağlar. |
| Kaynak | Kaynak açılan kutusunda seçilen kaynağı varsayılan olarak, paket kaynağı. |
| Lisans | Tarayıcıyı paketin lisans URL 'SI için açar. Lisans ya da-ReportAbuse belirtilmediyse, tarayıcı paketin proje URL 'sini açar. |
| ReportAbuse | Tarayıcıyı paketin uygunsuz kullanım URL 'SI için açar. Lisans ya da-ReportAbuse belirtilmediyse, tarayıcı paketin proje URL 'sini açar. |
| PassThru | URL 'YI görüntüler; tarayıcının açılmasını engellemek için-whatIf ile kullanın. |

Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.

## <a name="common-parameters"></a>Ortak Parametreler

`Open-PackagePage` Şu [ortak PowerShell parametrelerini](/powershell/module/microsoft.powershell.core/about/about_commonparameters)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.

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