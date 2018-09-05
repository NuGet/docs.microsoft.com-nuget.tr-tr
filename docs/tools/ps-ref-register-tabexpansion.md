---
title: NuGet Register-TabExpansion PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolu kayıt TabExpansion PowerShell komutunda referansı.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 98171c598bd4a3468bd23e2d6060e267c38021b4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546611"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (Visual Studio'da Paket Yöneticisi Konsolu)

*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da.*

Belirtilen komut parametreleri için bir sekme genişletmeyi sekmesini komutu girerken kullanıldığında, söz konusu parametresi için kullanılabilir seçenekler olarak genişletilmiş değerlerin göründüğü şekilde kaydeder. Komut için önceki tüm genişletmeleri üzerine yazılır.

## <a name="syntax"></a>Sözdizimi

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Ad | (Gerekli) Hangi genişletmeleri kaydetmek komutu. -Name anahtarın kendisinde, isteğe bağlıdır. |
| Tanım | (Gerekli) Bağımsız değişken söz diziminde açıklayan bir nesne `@{'<parameter>' = {'<value1>', '<value2>', ...}}` burada `<parameter>` değiştirmek için parametre ve her adıdır `<value>` belirli bir genişletme sağlar. Tek ve çift tırnak işaretleri kabul edilir. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.

## <a name="common-parameters"></a>Ortak parametreleri

`Register-TabExpansion` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntılı, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

Üç projeleri adları EventManager ve yardımcı programları SpecialParser içeren bir çözümü göz önünde bulundurun. Geliştirici sık kullandığı `Update-Package` ile bu projelerin her biri farklı zamanlarda komutu. Kendisi kullanışlı bulur `Update-Package` komut sağlamak için otomatik tamamlama genişletmeleri `-ProjectName` her zaman bir proje adı yazabileceğiniz geliştirmiyor bu yüzden bağımsız değişken. 

Aşağıdaki komutu, bu üç proje adları için bir genişletme olarak daha sonra kaydeder `-ProjectName` parametresi:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Geliştirici ardından yazabilirsiniz `Update-Package -ProjectName `SEKME tuşuna basın ve Otomatik Tamamlama seçeneği olarak sunulan genişletmeleri bakın:

![Register-TabExpansion kullanma örneği](media/Register-TabExpansion-Example.png)
