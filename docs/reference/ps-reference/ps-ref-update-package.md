---
title: NuGet Update-Package PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Update-Package PowerShell komutuna yönelik başvuru.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 159817e56d978d6432e989d2027907c0d2445222
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777383"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (Visual Studio 'da Paket Yöneticisi konsolu)

*Yalnızca Windows üzerinde Visual Studio 'daki [NuGet Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*

Bir paketi ve onun bağımlılıklarını veya bir projedeki tüm paketleri daha yeni bir sürüme güncelleştirir.

## <a name="syntax"></a>Syntax

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

NuGet 2.8 + ' de, `Update-Package` projenizde var olan bir paketin indirgenmesini sağlamak için kullanılabilir. Örneğin, Microsoft. AspNet. MVC 5.1.0-RC1 yüklüyse, aşağıdaki komut bunu 5.0.0 'e indirgeyebilecek:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametreler

|  Parametre | Açıklama |
| --- | --- |
| Id | Güncelleştirilecek paketin tanımlayıcısı. Atlanırsa, tüm paketleri güncelleştirir. -ID anahtarı isteğe bağlıdır. |
| Ignoredependencies | Paketin bağımlılıklarını güncelleştirmeyi atlar. |
| ProjectName | Güncelleştirilecek paketleri içeren projenin adı, tüm projeleri varsayılan olarak içerir. |
| Sürüm | Yükseltme için kullanılacak sürüm, en son sürüme varsayılan olarak ayarlanıyor. NuGet 3.0 + sürümünde sürüm değeri *En düşük, en yüksek, HighestMinor* veya *HighestPatch* (-Safe) olmalıdır. |
| Güven | Yükseltmeleri, şu anda yüklü olan paket ile aynı ana ve alt sürümü olan sürümlerle kısıtlar. |
| Kaynak | Aranacak paket kaynağının URL veya klasör yolu. Yerel klasör yolları mutlak veya geçerli klasöre göreli olabilir. Atlanırsa, `Update-Package` Şu anda seçili olan paket kaynağını arar. |
| Includeönsürümü | Güncelleştirmeler için yayın öncesi paketleri içerir. |
| Yeniden yükleme | Paketleri şu anda yüklü sürümlerini kullanarak resintalls. Bkz. [paketleri yeniden yükleme ve güncelleştirme](../../consume-packages/reinstalling-and-updating-packages.md). |
| FileConflictAction | Proje tarafından başvurulan var olan dosyaların üzerine yazılması veya yoksayılması istendiğinde gerçekleştirilecek eylem. Olası değerler *üzerine yazılır, Yoksay, None, overwriteall* ve *IgnoreAll* (3.0 +). |
| DependencyVersion | Kullanılacak bağımlılık paketlerinin sürümü, bu, aşağıdakilerden biri olabilir:<br/><ul><li>*En düşük* (varsayılan): en düşük sürüm</li><li>*HighestPatch*: en düşük ana, en düşük ikincil, en yüksek düzeltme eki olan sürüm</li><li>*HighestMinor*: en düşük ana, en yüksek ikincil, en yüksek düzeltme eki olan sürüm</li><li>*En yüksek* (parametresiz Update-Package için varsayılan): en yüksek sürüm</li></ul>Varsayılan değeri, [`dependencyVersion`](../nuget-config-file.md#config-section) dosyadaki ayarını kullanarak ayarlayabilirsiniz `Nuget.Config` . |
| ToHighestPatch | -Safe ile eşdeğerdir. |
| ToHighestMinor | Yükseltmeleri yalnızca, yüklü olan paketle aynı ana sürüme sahip sürümlere kısıtlar. |
| WhatIf | Gerçekten güncelleştirmeyi gerçekleştirmeden, komutu çalıştırırken ne olacağını gösterir. |

Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.

### <a name="common-parameters"></a>Ortak Parametreler

`Update-Package` Şu [ortak PowerShell parametrelerini](/powershell/module/microsoft.powershell.core/about/about_commonparameters)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.

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
Update-Package Elmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package Elmah –reinstall -ignoreDependencies
```
