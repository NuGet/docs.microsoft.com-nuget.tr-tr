---
title: "NuGet ekleme BindingRedirect PowerShell başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 90f4dcb0-6e5a-4948-8ea9-62e0d061d95a
description: "Visual Studio'da NuGet Paket Yöneticisi konsolunda Ekle BindingRedirect PowerShell komut başvurusu."
keywords: "NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu, Add-BindingRedirect"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7bf8cdb938195f4747932b38ef0d5bb6c34b9137
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Ekleme BindingRedirect (Visual Studio'da Paket Yöneticisi Konsolu)

*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](Package-Manager-Console.md) Windows Visual Studio'da.*

Bir proje için çıkış yolu içindeki tüm derlemelerde arar ve gerektiğinde uygulama veya web yapılandırma dosyasına bağlama yeniden yönlendirmelerini ekler. Bu komut, bir paket yüklerken otomatik olarak çalıştırılır.

Bağlama yeniden yönlendirmeleri ve neden kullanıldıkları hakkında ayrıntılar için bkz: [derleme sürümlerini yönlendirme](https://docs.microsoft.com/dotnet/framework/configure-apps/redirect-assembly-versions) .NET belgelerinde.

## <a name="syntax"></a>Sözdizimi

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| ProjectName | (Gerekli) Bağlama yeniden yönlendirmeleri eklenecek projesi. -ProjectName anahtar isteğe bağlıdır. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.

## <a name="common-parameters"></a>Ortak parametreleri

`Add-BindingRedirect`Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```