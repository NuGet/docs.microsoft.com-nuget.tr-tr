---
title: "NuGet paket PowerShell başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio'da NuGet Paket Yöneticisi konsolunda güncelleştirme paketini PowerShell komut başvurusu."
keywords: "NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu, güncelleştirme paketi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 293d9a7fdcce633eb5a97e5f76398deb5c13bdb4
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/08/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Güncelleştirme Paketi (Visual Studio'da Paket Yöneticisi Konsolu)

*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da.*

Bir paketi ve bağımlılıklarını ya da bir projesindeki tüm paketleri daha yeni bir sürüme güncelleştirir.

## <a name="syntax"></a>Sözdizimi

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

NuGet 2.8 + içinde `Update-Package` var olan bir paketini projenize düşürmek için kullanılabilir. Microsoft.AspNet.MVC 5.1.0-rc1 yüklü varsa, örneğin, aşağıdaki komut, 5.0.0 için düşürmek:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametreler

|  Parametre | Açıklama |
| --- | --- |
| Kimliği | Güncelleştirilecek paket tanımlayıcısı. Atlanırsa, tüm paketleri güncelleştirir. Kimliği anahtarı kendisini isteğe bağlı değil. |
| IgnoreDependencies | Paketin bağımlılıklarını güncelleştirme atlar. |
| ProjectName | Güncelleştirilecek paketi içeren, tüm projeler için varsayılan değer olarak projesinin adı. |
| Sürüm | En son sürüm varsayılan değer olarak, yükseltme için kullanılacak sürümü. NuGet içinde 3.0 +, sürüm değeri şunlardan biri olmalıdır *en düşük, en yüksek, HighestMinor*, veya *HighestPatch* (eşdeğer - güvenli). |
| Güvenli | Yükseltmeleri aynı birincil ve ikincil sürüme yüklü paketi içeren yalnızca sürümlerle kısıtlar. |
| Kaynak | Aranacak paket kaynağının URL'sini veya klasör yolu. Yerel klasör yolları mutlak veya göreli geçerli klasörde olabilir. Atlanırsa, `Uninstall-Package` şu anda seçili paket kaynağını arar. |
| IncludePrerelease | Yayın öncesi paketleri için güncelleştirmeleri içerir. |
| Yeniden yükleme | Şu anda yüklü sürümlerine kullanarak Resintalls paketler. Bkz: [Reinstalling ve paketleri güncelleştiriliyor](../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | Üzerine veya varolan dosyaları proje tarafından başvurulan yoksayar istenir olduğunda gerçekleştirilecek eylem. Olası değerler şunlardır: *üzerine yazma, yoksay, None, OverwriteAll*, ve *IgnoreAll* (3.0 +). |
| DependencyVersion | Şunlardan biri olabilen kullanmak için bağımlılık Paket sürümü:<br/><ul><li>*En düşük* (varsayılan): en düşük sürüm</li><li>*HighestPatch*: en düşük ana, en düşük küçük, en yüksek düzeltme eki sürümüyle</li><li>*HighestMinor*: en düşük ana sürümle, en yüksek ikincil, en yüksek düzeltme eki</li><li>*En yüksek* (hiçbir parametre güncelleştirme paketi için varsayılan): en yüksek sürüm</li></ul>Varsayılan değer kullanılarak ayarlayabilirsiniz [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) ayarı `Nuget.Config` dosya. |
| ToHighestPatch | Yalnızca şu anda yüklenmiş paket ile aynı ikincil sürümle sürümlerine yükseltme kısıtlar. |
| ToHighestMinor | Yalnızca şu anda yüklü paketi olarak aynı ana sürümüne sürümleriyle yükseltmeleri kısıtlar. |
| WhatIf | Komut gerçekte güncelleştirme yapmadan çalıştırırken ne olacağını gösterir. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.

### <a name="common-parameters"></a>Ortak parametreleri

`Update-Package` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.

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