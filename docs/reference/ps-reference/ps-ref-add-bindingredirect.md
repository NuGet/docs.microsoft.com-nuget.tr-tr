---
title: NuGet Add-BindingRedirect PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Add-BindingRedirect PowerShell komutuna yönelik başvuru.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 62edf1bf8995a4e1ffb83acc7a7621a786cc53e4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777612"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (Visual Studio 'da Paket Yöneticisi konsolu)

*Yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*

Bir projenin çıkış yolundaki tüm derlemeleri inceler ve gerektiğinde uygulamaya veya Web yapılandırma dosyasına bağlama yeniden yönlendirmeleri ekler. Bu komut, bir paket yüklenirken otomatik olarak çalıştırılır.

> [!NOTE]
> Bu yalnızca bir packages.config dosyası kullanan senaryolar için geçerlidir. Daha fazla bilgi için bkz. [NuGet packages.config dosya başvurusu](~/reference/packages-config.md).

Bağlama yeniden yönlendirmeleri ve bunların kullanılma nedenleri hakkında daha fazla bilgi için bkz. .NET belgelerindeki [derleme sürümlerini yeniden yönlendirme](/dotnet/framework/configure-apps/redirect-assembly-versions) .

## <a name="syntax"></a>Sözdizimi

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| ProjectName | Istenir Bağlama yeniden yönlendirmelerinin ekleneceği proje. -ProjectName anahtarı isteğe bağlıdır. |

Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.

## <a name="common-parameters"></a>Ortak Parametreler

`Add-BindingRedirect` Şu [ortak PowerShell parametrelerini](/powershell/module/microsoft.powershell.core/about/about_commonparameters)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```