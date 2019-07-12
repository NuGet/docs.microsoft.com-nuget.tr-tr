---
title: NuGet eşitleme-Package PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi Konsolu'nda eşitleme-Package PowerShell komutunu referansı.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: de0b612e1335cafdcd6a0b802d54f2182d27ad22
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842256"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Visual Studio'da Paket Yöneticisi Konsolu)

*Sürüm 3.0 +; yalnızca içinde kullanılabilir [Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da.*

Yüklü Paket sürümü belirtilen (veya varsayılan) alır, proje ve çözümdeki projelerin geri kalanı sürümüne eşitler.

## <a name="syntax"></a>Sözdizimi

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Id | (Gerekli) Eşitlenecek paket tanımlayıcısı. Kimliği anahtarın kendisinde, isteğe bağlıdır. |
| IgnoreDependencies | Yalnızca bu paket ve onun bağımlılıklarını yükleyin. |
| ProjectName | Varsayılan proje için varsayılan olarak ayarlanıyor paketi, eşitleme için proje. |
| Sürüm | Eşitlemek için paketin sürümü yüklü sürümü için varsayılan olarak ayarlanıyor. |
| Source | Aranacak paket kaynağı için URL veya klasör yolu. Yerel klasör yol mutlak veya göreli geçerli klasörde olabilir. Atlanırsa, `Sync-Package` seçili paket kaynağı arar. |
| IncludePrerelease | Yayın öncesi paketleri Eşitle içerir. |
| FileConflictAction | Üzerine ya da proje tarafından başvurulan mevcut dosyaları yoksaymak için sorulan olduğunda gerçekleştirilecek eylem. Olası değerler *üzerine yaz, yoksay, None, OverwriteAll*, ve *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | Aşağıdakilerden biri olabilen kullanmak için bağımlılık paketlerini sürümü:<br/><ul><li>*En düşük* (varsayılan): en düşük sürüm</li><li>*HighestPatch*: en düşük büyük, en düşük küçük, yüksek düzeltme sürümü</li><li>*HighestMinor*: en düşük ana sürümle, en yüksek ikincil, yüksek düzeltme eki</li><li>*En yüksek* (parametre olmadan Update-Package için varsayılan): en yüksek sürüm</li></ul>Varsayılan değer kullanarak ayarlayabilirsiniz [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) ayarı `Nuget.Config` dosya. |
| WhatIf | Eşitleme işlemini gerçekleştirmeden komutu çalıştırırken ne olacağını gösterir. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.

## <a name="common-parameters"></a>Ortak parametreleri

`Sync-Package` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): Hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, ayrıntılı PipelineVariable, WarningAction ve WarningVariable.

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
