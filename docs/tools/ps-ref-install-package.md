---
title: NuGet Install-Package PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda Install-Package PowerShell komut başvurusu.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5adfbcae0affcaa402f7981c12e108490d546511
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Visual Studio'da Paket Yöneticisi Konsolu)

*Bu konu içindeki komut açıklar [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da. Genel PowerShell Install-Package komutu için bkz: [PowerShell PackageManagement başvuru](/powershell/module/packagemanagement/?view=powershell-6).*

Bir paketi ve bağımlılıklarını projeye yükler.

## <a name="syntax"></a>Sözdizimi

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

NuGet 2.8 + içinde `Install-Package` projenizi mevcut bir pakete düşebilen. Microsoft.AspNet.MVC 5.1.0-rc1 yüklü varsa, örneğin, aşağıdaki komut, 5.0.0 için düşürmek:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Kimliği | (Gerekli) Yüklenecek paket tanımlayıcısı. (*3.0 +*) tanımlayıcı bir yolu veya URL'si olabilir bir `packages.config` dosya veya bir `.nupkg` dosyası. Kimliği anahtarı kendisini isteğe bağlı değil. |
| IgnoreDependencies | Yalnızca bu paketi ve bağımlılıklarını yükleyin. |
| ProjectName | Projeye varsayılan proje için varsayılan değer olarak paketin yükleneceği. |
| Kaynak | Aranacak paket kaynağının URL'sini veya klasör yolu. Yerel klasör yolları mutlak veya göreli geçerli klasörde olabilir. Atlanırsa, `Install-Package` şu anda seçili paket kaynağını arar. |
| Sürüm | Yüklemek için paketin sürümü en son sürüm varsayılan olarak ayarlanıyor. |
| IncludePrerelease | Yükleme için ön sürüm paketlerini göz önünde bulundurur. Atlanırsa, yalnızca kalıcı paketler değerlendirilir. |
| FileConflictAction | Üzerine veya varolan dosyaları proje tarafından başvurulan yoksayar istenir olduğunda gerçekleştirilecek eylem. Olası değerler şunlardır: *üzerine yazma, yoksay, None, OverwriteAll*, ve *(3.0 +)* *IgnoreAll*. |
| DependencyVersion | Şunlardan biri olabilen kullanmak için bağımlılık Paket sürümü:<br/><ul><li>*En düşük* (varsayılan): en düşük sürüm</li><li>*HighestPatch*: en düşük ana, en düşük küçük, en yüksek düzeltme eki sürümüyle</li><li>*HighestMinor*: en düşük ana sürümle, en yüksek ikincil, en yüksek düzeltme eki</li><li>*En yüksek* (hiçbir parametre güncelleştirme paketi için varsayılan): en yüksek sürüm</li></ul>Varsayılan değer kullanılarak ayarlayabilirsiniz [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) ayarı `Nuget.Config` dosya. |
| WhatIf | Komut gerçekte yükleme yapmadan çalıştırırken ne olacağını gösterir. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.

## <a name="common-parameters"></a>Ortak parametreleri

`Install-Package` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.

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