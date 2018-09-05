---
title: NuGet paket PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolu Update-Package PowerShell komutunda referansı.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d47e1978ab7d827e0b8b97cd4e7237019185b50f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546082"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (Visual Studio'da Paket Yöneticisi Konsolu)

*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da.*

Bir paketi ve bağımlılıkları veya bir projedeki tüm paketleri yeni bir sürüme güncelleştirir.

## <a name="syntax"></a>Sözdizimi

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

Nuget'te 2.8 + `Update-Package` projenizdeki varolan paketi düşürmek için kullanılabilir. Yüklü Microsoft.AspNet.MVC 5.1.0-rc1 varsa, örneğin, aşağıdaki komut, 5.0.0 için düşürme:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametreler

|  Parametre | Açıklama |
| --- | --- |
| Kimliği | Güncelleştirilecek paket tanımlayıcısı. Atlanırsa, tüm paketleri güncelleştirir. Kimliği anahtarın kendisinde, isteğe bağlıdır. |
| IgnoreDependencies | Paket bağımlılıkları güncelleştirme atlar. |
| ProjectName | Güncelleştirme paketlerini içeren, tüm projeler için varsayılan olarak ayarlanıyor. proje adı. |
| Sürüm | Varsayılan en son sürüme yükseltme için kullanılacak sürümü. Nuget'te 3.0 +, sürüm değeri şunlardan biri olmalıdır *en düşük, en yüksek HighestMinor*, veya *HighestPatch* (eşdeğer - güvenli). |
| Güvenli | Yalnızca şu anda yüklü paketleri aynı birincil ve ikincil sürüme sürümleriyle yükseltmeleri kısıtlar. |
| Kaynak | Aranacak paket kaynağı için URL veya klasör yolu. Yerel klasör yol mutlak veya göreli geçerli klasörde olabilir. Atlanırsa, `Update-Package` seçili paket kaynağı arar. |
| IncludePrerelease | Yayın öncesi paketleri için güncelleştirmeleri içerir. |
| Yeniden yükleyin | Şu anda yüklü sürümlerini kullanarak Resintalls paketleri. Bkz: [Reinstalling ve paketlerin güncelleştirilmesi](../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | Üzerine ya da proje tarafından başvurulan mevcut dosyaları yoksaymak için sorulan olduğunda gerçekleştirilecek eylem. Olası değerler *üzerine yaz, yoksay, None, OverwriteAll*, ve *IgnoreAll* (3.0 +). |
| DependencyVersion | Aşağıdakilerden biri olabilen kullanmak için bağımlılık paketlerini sürümü:<br/><ul><li>*En düşük* (varsayılan): en düşük sürüm</li><li>*HighestPatch*: en düşük büyük, en düşük küçük, yüksek düzeltme sürümü</li><li>*HighestMinor*: en düşük ana sürümle, en yüksek ikincil, yüksek düzeltme eki</li><li>*En yüksek* (parametre olmadan Update-Package için varsayılan): en yüksek sürüm</li></ul>Varsayılan değer kullanarak ayarlayabilirsiniz [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) ayarı `Nuget.Config` dosya. |
| ToHighestPatch | Yalnızca aynı alt sürümü şu anda yüklü paketleri olarak sürümleriyle yükseltmeleri kısıtlar. |
| ToHighestMinor | Yükseltmeleri yalnızca sürümleri şu anda yüklü paketleri ile aynı ana sürümle kısıtlar. |
| WhatIf | Komut güncelleştirme yapmadan çalıştırılırken ne olacağını gösterir. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.

### <a name="common-parameters"></a>Ortak parametreleri

`Update-Package` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntılı, WarningAction ve WarningVariable.

### <a name="examples"></a>Örnekler

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
