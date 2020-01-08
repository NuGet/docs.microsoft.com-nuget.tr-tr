---
title: NuGet Sync-Package PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Sync-Package PowerShell komutu için başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 12a3d5f32056539a75da9e17b15d67e72a8a42c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384909"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Visual Studio'da Paket Yöneticisi Konsolu)

*Sürüm 3.0 +; yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*

Belirtilen (veya varsayılan) projeden yüklü paketin sürümünü alır ve sürümü çözümdeki diğer projelere eşitler.

## <a name="syntax"></a>Sözdizimi

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Id | Istenir Eşitlenecek paketin tanımlayıcısı. -ID anahtarı isteğe bağlıdır. |
| Ignoredependencies | Yalnızca bu paketi yükler ve bağımlılıklarını değil. |
| ProjectName | Paketi eşitlenecek proje, varsayılan proje varsayılan olarak varsayılan projem. |
| Sürüm | Eşitlenecek paketin sürümü, şu anda yüklü olan sürüme dönülüyor. |
| Kaynak | Aranacak paket kaynağının URL veya klasör yolu. Yerel klasör yolları mutlak veya geçerli klasöre göreli olabilir. Atlanırsa, `Sync-Package` Şu anda seçili olan paket kaynağını arar. |
| Includeönsürümü | Eşitlenmiş yayın öncesi paketleri içerir. |
| FileConflictAction | Proje tarafından başvurulan var olan dosyaların üzerine yazılması veya yoksayılması istendiğinde gerçekleştirilecek eylem. Olası değerler *üzerine yazılır, Yoksay, None, overwriteall*ve *(3,0 +)* *IgnoreAll*. |
| DependencyVersion | Kullanılacak bağımlılık paketlerinin sürümü, bu, aşağıdakilerden biri olabilir:<br/><ul><li>*En düşük* (varsayılan): en düşük sürüm</li><li>*HighestPatch*: en düşük ana, en düşük ikincil, en yüksek düzeltme eki olan sürüm</li><li>*HighestMinor*: en düşük ana, en yüksek ikincil, en yüksek düzeltme eki olan sürüm</li><li>*En yüksek* (parametresi olmayan Update-Package için varsayılan): en yüksek sürüm</li></ul>`Nuget.Config` dosyasındaki [`dependencyVersion`](../nuget-config-file.md#config-section) ayarını kullanarak varsayılan değeri ayarlayabilirsiniz. |
| WhatIf | Komutu, eşitlemeyi gerçekten gerçekleştirmeden çalışırken ne olacağını gösterir. |

Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.

## <a name="common-parameters"></a>Ortak Parametreler

`Sync-Package`, şu [ortak PowerShell parametrelerini](https://go.microsoft.com/fwlink/?LinkID=113216)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
