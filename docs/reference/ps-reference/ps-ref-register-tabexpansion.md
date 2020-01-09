---
title: NuGet Register-Tabgenişleme PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Register-Tabgenişleme PowerShell komutuna yönelik başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384460"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-Tabgenişleme (Visual Studio 'da Paket Yöneticisi konsolu)

*Yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*

Belirtilen komutun parametreleri için bir sekme genişletmesi kaydeder, örneğin bir komut girerken Tab kullanıldığında, genişletilmiş değerler söz konusu parametre için kullanılabilir seçenekler olarak görünür. Komutun önceki genişletmeleri üzerine yazılır.

## <a name="syntax"></a>Sözdizimi

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Name | Istenir Expansions 'in kaydedileceği komut. -Name anahtarı isteğe bağlıdır. |
| Tanım | Istenir Söz diziminde bağımsız değişkeni tanımlayan bir nesne, `<parameter>` değiştirilecek parametrenin adı `@{'<parameter>' = {'<value1>', '<value2>', ...}}` ve her `<value>` belirli bir genişletme sağlar. Hem tek hem de çift tırnak işareti kabul edilir. |

Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.

## <a name="common-parameters"></a>Ortak Parametreler

`Register-TabExpansion`, şu [ortak PowerShell parametrelerini](https://go.microsoft.com/fwlink/?LinkID=113216)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

EventManager, yardımcı programlar ve SpecialParser olmak üzere üç proje adı içeren bir çözüm düşünün. Geliştirici genellikle `Update-Package` komutunu bu projelerin her biriyle farklı zamanlarda kullanır. `Update-Package` komutunun, `-ProjectName` bağımsız değişkeni için otomatik tamamlama genişletmeleri sağlamasına uygun olduğunu tespit eder; böylece her seferinde bir proje adı yazmak zorunda kalmaz. 

Aşağıdaki komut, bu üç proje adını `-ProjectName` parametresi için bir genişletme olarak kaydeder:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Geliştirici daha sonra `Update-Package -ProjectName `yazabilir, sekme tuşuna basabilir ve otomatik tamamlama seçenekleri olarak sunulan genişletmeleri görebilirler:

![Register-Tabgenişletmesini kullanma örneği](media/Register-TabExpansion-Example.png)
