---
title: "NuGet Register-TabExpansion PowerShell başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 8314ec69-ee8c-4933-84ef-e6d8a412d268
description: "Visual Studio'da NuGet Paket Yöneticisi konsolunda Register-TabExpansion PowerShell komut başvurusu."
keywords: "NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu, Register-TabExpansion"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 498b8638c81b800e5f20f7604b36e6af76da0283
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (Visual Studio'da Paket Yöneticisi Konsolu)

*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](Package-Manager-Console.md) Windows Visual Studio'da.*

Sekme komutu girerken kullanıldığında genişletilmiş değerler söz konusu parametre için kullanılabilir seçenekleri görünür olacağı şekilde bir sekme genişlemesi parametreler için belirtilen komut kaydeder. Komutu için önceki tüm genişletmeleri üzerine yazılır.

## <a name="syntax"></a>Sözdizimi

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Ad | (Gerekli) Hangi genişletmeleri kaydetmek komutu. -Name anahtarı kendisini isteğe bağlı değil. |
| Tanım | (Gerekli) Sözdizimi değişkeninde açıklayan bir nesne `@{'<parameter>' = {'<value1>', '<value2>', ...}}` nerede `<parameter>` değiştirmek için parametre ve her adıdır `<value>` belirli bir genişletme sağlar. Tek ve çift tırnak işaretleri kabul edilir. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.

## <a name="common-parameters"></a>Ortak parametreleri

`Register-TabExpansion`Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

Üç projeleri adları EventManager, yardımcı programlar ve SpecialParser içeren bir çözüm göz önünde bulundurun. Geliştirici sık kullandığı `Update-Package` bu projelerin her biri ile farklı zamanlarda komutu. Kendisi kullanışlı bulur `Update-Package` komutu sağlamak için otomatik tamamlama genişletmeleri `-ProjectName` kendisi her zaman bir proje adı yazın gerekmez şekilde bağımsız değişkeni. 

Aşağıdaki komutu için bir genişletme bu üç proje adları daha sonra kaydeder `-ProjectName` parametre:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Geliştirici ardından yazabilirsiniz `Update-Package -ProjectName `SEKME tuşuna basın ve otomatik tamamlama seçenekleri olarak sunulan genişletmeler bakın:

![Register-TabExpansion kullanma örneği](media/Register-TabExpansion-Example.png)
