---
title: NuGet Register-Tabgenişleme PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Register-Tabgenişleme PowerShell komutuna yönelik başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 14cda695677e1052c78169fda097b72b460a9d43
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328194"
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
| Ad | Istenir Expansions 'in kaydedileceği komut. -Name anahtarı isteğe bağlıdır. |
| Tanım | Istenir Söz dizimi `@{'<parameter>' = {'<value1>', '<value2>', ...}}` `<value>` içindeki bağımsız değişkeni tanımlayan bir nesne, değiştirilecek parametrenin adı ,herbiribelirlibirgenişletmesağlar.`<parameter>` Hem tek hem de çift tırnak işareti kabul edilir. |

Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.

## <a name="common-parameters"></a>Ortak Parametreler

`Register-TabExpansion`Aşağıdaki [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, verbose, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

EventManager, yardımcı programlar ve SpecialParser olmak üzere üç proje adı içeren bir çözüm düşünün. Geliştirici genellikle `Update-Package` komutu bu projelerin her biriyle farklı zamanlarda kullanır. `Update-Package` Komutun her seferinde bir proje adı yazmasının gerekmemesi için `-ProjectName` bağımsız değişken için otomatik tamamlama genişletmeleri sağlamasına uygun olduğunu buluyor. 

Aşağıdaki komut, bu üç proje adını `-ProjectName` parametresi için bir genişletme olarak kaydeder:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

Daha sonra geliştirici yazabilir `Update-Package -ProjectName `, sekme tuşuna basabilir ve otomatik tamamlama seçenekleri olarak sunulan genişletmeleri görebilirler:

![Register-Tabgenişletmesini kullanma örneği](media/Register-TabExpansion-Example.png)
