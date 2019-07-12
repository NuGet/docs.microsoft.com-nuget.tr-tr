---
title: NuGet Register-TabExpansion PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolu kayıt TabExpansion PowerShell komutunda referansı.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8adb80af85e2e32fa8c35e5272cf90ff0c0ddcbb
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842489"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (Visual Studio'da Paket Yöneticisi Konsolu)

*Yalnızca içinde kullanılabilir [Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da.*

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

`Register-TabExpansion` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): Hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, ayrıntılı PipelineVariable, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

Üç projeleri adları EventManager ve yardımcı programları SpecialParser içeren bir çözümü göz önünde bulundurun. Geliştirici sık kullandığı `Update-Package` ile bu projelerin her biri farklı zamanlarda komutu. Kendisi kullanışlı bulur `Update-Package` komut sağlamak için otomatik tamamlama genişletmeleri `-ProjectName` her zaman bir proje adı yazabileceğiniz geliştirmiyor bu yüzden bağımsız değişken. 

Aşağıdaki komutu, bu üç proje adları için bir genişletme olarak daha sonra kaydeder `-ProjectName` parametresi:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Geliştirici ardından yazabilirsiniz `Update-Package -ProjectName `SEKME tuşuna basın ve Otomatik Tamamlama seçeneği olarak sunulan genişletmeleri bakın:

![Register-TabExpansion kullanma örneği](media/Register-TabExpansion-Example.png)
