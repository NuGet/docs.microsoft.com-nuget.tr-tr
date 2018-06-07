---
title: NuGet Register-TabExpansion PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda Register-TabExpansion PowerShell komut başvurusu.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8011c0e6aa951a32114d460803c493810964a7e0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818424"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (Visual Studio'da Paket Yöneticisi Konsolu)

*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da.*

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

`Register-TabExpansion` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

Üç projeleri adları EventManager, yardımcı programlar ve SpecialParser içeren bir çözüm göz önünde bulundurun. Geliştirici sık kullandığı `Update-Package` bu projelerin her biri ile farklı zamanlarda komutu. Kendisi kullanışlı bulur `Update-Package` komutu sağlamak için otomatik tamamlama genişletmeleri `-ProjectName` kendisi her zaman bir proje adı yazın gerekmez şekilde bağımsız değişkeni. 

Aşağıdaki komutu için bir genişletme bu üç proje adları daha sonra kaydeder `-ProjectName` parametre:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Geliştirici ardından yazabilirsiniz `Update-Package -ProjectName `SEKME tuşuna basın ve otomatik tamamlama seçenekleri olarak sunulan genişletmeler bakın:

![Register-TabExpansion kullanma örneği](media/Register-TabExpansion-Example.png)
