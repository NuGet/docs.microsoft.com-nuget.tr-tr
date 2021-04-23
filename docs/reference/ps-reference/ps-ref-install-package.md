---
title: NuGet Install-Package PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Install-Package PowerShell komutuna yönelik başvuru.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ad551b8701cfc2061f7721fb050ed9b5a4fede32
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901700"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Visual Studio 'da Paket Yöneticisi konsolu)

*Bu konuda, Windows üzerinde Visual Studio 'da [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içindeki komut açıklanmaktadır. Genel PowerShell Install-Package komutu için bkz. [PowerShell PackageManagement başvurusu](/powershell/module/packagemanagement).*

Bir paketi ve bağımlılıklarını bir projeye kurar.

## <a name="syntax"></a>Syntax

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

NuGet 2.8 + ' de, `Install-Package` projenizdeki mevcut bir paketin indirgenmesini sağlayabilir. Örneğin, Microsoft. AspNet. MVC 5.1.0-RC1 yüklüyse, aşağıdaki komut bunu 5.0.0 'e indirgeyebilecek:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Id | Istenir Yüklenecek paketin tanımlayıcısı. (*3.0 +*) Tanımlayıcı, bir dosyanın veya dosyanın bir yolu veya URL 'SI olabilir `packages.config` `.nupkg` . -ID anahtarı isteğe bağlıdır. |
| Ignoredependencies | Yalnızca bu paketi yükler ve bağımlılıklarını değil. |
| ProjectName | Paketin yükleneceği proje, varsayılan projenin varsayılan bir proje olur. |
| Kaynak | Aranacak paket kaynağının URL veya klasör yolu. Yerel klasör yolları mutlak veya geçerli klasöre göreli olabilir. Atlanırsa, `Install-Package` Şu anda seçili olan paket kaynağını arar. |
| Sürüm | Yüklenecek paketin sürümü, en son sürümü varsayılan olarak sağlar. |
| Includeönsürümü | Yüklemenin yayın öncesi paketlerini dikkate alır. Atlanırsa, yalnızca kararlı paketler değerlendirilir. |
| FileConflictAction | Proje tarafından başvurulan var olan dosyaların üzerine yazılması veya yoksayılması istendiğinde gerçekleştirilecek eylem. Olası değerler *üzerine yazılır, Yoksay, None, overwriteall* ve *(3,0 +)* *IgnoreAll*. |
| DependencyVersion | Kullanılacak bağımlılık paketlerinin sürümü, bu, aşağıdakilerden biri olabilir:<br/><ul><li>*En düşük* (varsayılan): en düşük sürüm</li><li>*HighestPatch*: en düşük ana, en düşük ikincil, en yüksek düzeltme eki olan sürüm</li><li>*HighestMinor*: en düşük ana, en yüksek ikincil, en yüksek düzeltme eki olan sürüm</li><li>*En yüksek* (parametresiz Update-Package için varsayılan): en yüksek sürüm</li></ul>Varsayılan değeri, [`dependencyVersion`](../nuget-config-file.md#config-section) dosyadaki ayarını kullanarak ayarlayabilirsiniz `Nuget.Config` . |
| WhatIf | Yüklemeyi yapmadan komutu çalıştırırken ne olacağını gösterir. |

Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.

## <a name="common-parameters"></a>Ortak Parametreler

`Install-Package` Şu [ortak PowerShell parametrelerini](/powershell/module/microsoft.powershell.core/about/about_commonparameters)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```