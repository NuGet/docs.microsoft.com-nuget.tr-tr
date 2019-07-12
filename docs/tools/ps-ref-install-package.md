---
title: NuGet Install-Package PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolu Install-Package PowerShell komutunda referansı.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 755c87bbc68d3b688c81e16edbc1faabdc9e0520
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842493"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Visual Studio'da Paket Yöneticisi Konsolu)

*Bu konu içindeki komut açıklar [Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da. Genel PowerShell Install-Package komutu için bkz: [PowerShell PackageManagement başvuru](/powershell/module/packagemanagement/?view=powershell-6).*

Bir projeye bir paketi ve bağımlılıkları yükler.

## <a name="syntax"></a>Sözdizimi

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

Nuget'te 2.8 + `Install-Package` projenizdeki varolan paketi düşürebilir. Yüklü Microsoft.AspNet.MVC 5.1.0-rc1 varsa, örneğin, aşağıdaki komut, 5.0.0 için düşürme:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Id | (Gerekli) Yüklenecek paket tanımlayıcısı. (*3.0 +* ) tanımlayıcı bir yol veya URL'sini olabilir bir `packages.config` dosya veya `.nupkg` dosya. Kimliği anahtarın kendisinde, isteğe bağlıdır. |
| IgnoreDependencies | Yalnızca bu paket ve onun bağımlılıklarını yükleyin. |
| ProjectName | Projeye varsayılan proje için varsayılan olarak ayarlanıyor, paketi yüklemek için. |
| Source | Aranacak paket kaynağı için URL veya klasör yolu. Yerel klasör yol mutlak veya göreli geçerli klasörde olabilir. Atlanırsa, `Install-Package` seçili paket kaynağı arar. |
| Sürüm | Yüklemek için paketin sürümü en son sürüme varsayılan olarak ayarlanıyor. |
| IncludePrerelease | Yayın öncesi paketleri yükleme için göz önünde bulundurur. Atlanırsa, yalnızca kararlı paket olarak kabul edilir. |
| FileConflictAction | Üzerine ya da proje tarafından başvurulan mevcut dosyaları yoksaymak için sorulan olduğunda gerçekleştirilecek eylem. Olası değerler *üzerine yaz, yoksay, None, OverwriteAll*, ve *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | Aşağıdakilerden biri olabilen kullanmak için bağımlılık paketlerini sürümü:<br/><ul><li>*En düşük* (varsayılan): en düşük sürüm</li><li>*HighestPatch*: en düşük büyük, en düşük küçük, yüksek düzeltme sürümü</li><li>*HighestMinor*: en düşük ana sürümle, en yüksek ikincil, yüksek düzeltme eki</li><li>*En yüksek* (parametre olmadan Update-Package için varsayılan): en yüksek sürüm</li></ul>Varsayılan değer kullanarak ayarlayabilirsiniz [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) ayarı `Nuget.Config` dosya. |
| WhatIf | Komut yükleme işlemi yapmadan çalıştırılırken ne olacağını gösterir. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.

## <a name="common-parameters"></a>Ortak parametreleri

`Install-Package` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): Hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, ayrıntılı PipelineVariable, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
