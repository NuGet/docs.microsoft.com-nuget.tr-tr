---
title: NuGet eşitleme-Package PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda eşitleme paket PowerShell komut başvurusu.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 92f0d7490dea57a69b5a5cb3cb7165f665f60d44
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818111"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Visual Studio'da Paket Yöneticisi Konsolu)

*Sürüm 3.0 +; yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da.*

Yüklü paketin sürümünü belirtilen (veya varsayılan) alır, proje ve sürümü çözümdeki projelerin geri kalanına eşitler.

## <a name="syntax"></a>Sözdizimi

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Kimliği | (Gerekli) Eşitlemek için paket tanımlayıcısı. Kimliği anahtarı kendisini isteğe bağlı değil. |
| IgnoreDependencies | Yalnızca bu paketi ve bağımlılıklarını yükleyin. |
| ProjectName | Varsayılan proje için varsayılan değer olarak paketinden, eşitleme projesi. |
| Sürüm | Eşitlemek için paketin sürümü şu anda yüklü olan sürümle varsayılan olarak ayarlanıyor. |
| Kaynak | Aranacak paket kaynağının URL'sini veya klasör yolu. Yerel klasör yolları mutlak veya göreli geçerli klasörde olabilir. Atlanırsa, `Sync-Package` şu anda seçili paket kaynağını arar. |
| IncludePrerelease | Ön sürüm paketlerini eşitleme içerir. |
| FileConflictAction | Üzerine veya varolan dosyaları proje tarafından başvurulan yoksayar istenir olduğunda gerçekleştirilecek eylem. Olası değerler şunlardır: *üzerine yazma, yoksay, None, OverwriteAll*, ve *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | Şunlardan biri olabilen kullanmak için bağımlılık Paket sürümü:<br/><ul><li>*En düşük* (varsayılan): en düşük sürüm</li><li>*HighestPatch*: en düşük ana, en düşük küçük, en yüksek düzeltme eki sürümüyle</li><li>*HighestMinor*: en düşük ana sürümle, en yüksek ikincil, en yüksek düzeltme eki</li><li>*En yüksek* (hiçbir parametre güncelleştirme paketi için varsayılan): en yüksek sürüm</li></ul>Varsayılan değer kullanılarak ayarlayabilirsiniz [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) ayarı `Nuget.Config` dosya. |
| WhatIf | Komut gerçekte eşitleme yapmadan çalıştırırken ne olacağını gösterir. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.

## <a name="common-parameters"></a>Ortak parametreleri

`Sync-Package` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.

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
