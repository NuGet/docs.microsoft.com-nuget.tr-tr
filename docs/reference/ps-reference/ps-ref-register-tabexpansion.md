---
title: NuGet Register-TabExpansion PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Register-TabExpansion PowerShell komutuna yönelik başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 9d5bae2878cb6bf0848bca9a5ed9af0fee61bb85
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237159"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (Visual Studio 'da Paket Yöneticisi konsolu)

*Yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*

Belirtilen komutun parametreleri için bir sekme genişletmesi kaydeder, örneğin bir komut girerken Tab kullanıldığında, genişletilmiş değerler söz konusu parametre için kullanılabilir seçenekler olarak görünür. Komutun önceki genişletmeleri üzerine yazılır.

## <a name="syntax"></a>Sözdizimi

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Ad | Istenir Expansions 'in kaydedileceği komut. -Name anahtarı isteğe bağlıdır. |
| Tanım | Istenir Söz dizimi içindeki bağımsız değişkeni tanımlayan bir nesne `@{'<parameter>' = {'<value1>', '<value2>', ...}}` , `<parameter>` Değiştirilecek parametrenin adı, her biri `<value>` belirli bir genişletme sağlar. Hem tek hem de çift tırnak işareti kabul edilir. |

Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.

## <a name="common-parameters"></a>Ortak Parametreler

`Register-TabExpansion` Şu [ortak PowerShell parametrelerini](/powershell/module/microsoft.powershell.core/about/about_commonparameters)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

EventManager, yardımcı programlar ve SpecialParser olmak üzere üç proje adı içeren bir çözüm düşünün. Geliştirici genellikle `Update-Package` komutu bu projelerin her biriyle farklı zamanlarda kullanır. `Update-Package`Komutun `-ProjectName` her seferinde bir proje adı yazmasının gerekmemesi için bağımsız değişken için otomatik tamamlama genişletmeleri sağlamasına uygun olduğunu buluyor. 

Aşağıdaki komut, bu üç proje adını parametresi için bir genişletme olarak kaydeder `-ProjectName` :

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Daha sonra geliştirici yazabilir `Update-Package -ProjectName ` , sekme tuşuna basabilir ve otomatik tamamlama seçenekleri olarak sunulan genişletmeleri görebilirler:

![Register-TabExpansion kullanma örneği](media/Register-TabExpansion-Example.png)