---
title: NuGet ekleme BindingRedirect PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolu Ekle BindingRedirect PowerShell komutunda referansı.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5f318ddfb2bb8498ab3e608f8036be05dcb0706
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842534"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (Visual Studio'da Paket Yöneticisi Konsolu)

*Yalnızca içinde kullanılabilir [Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da.*

Çıkış yolu için bir proje içindeki tüm derlemeleri inceler ve gerektiğinde uygulama veya web yapılandırma dosyasına bağlama yeniden yönlendirmeleri ekler. Bu komut, bir paket yükleme sırasında otomatik olarak çalıştırılır.

Yeniden yönlendirir ve neden kullanılır bağlama hakkında daha fazla bilgi için bkz [derleme sürümlerini yeniden yönlendirme](/dotnet/framework/configure-apps/redirect-assembly-versions) .NET belgelerinde.

## <a name="syntax"></a>Sözdizimi

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| ProjectName | (Gerekli) Hangi bağlama yeniden yönlendirmeleri eklemek proje. -ProjectName anahtar isteğe bağlıdır. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.

## <a name="common-parameters"></a>Ortak parametreleri

`Add-BindingRedirect` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): Hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, ayrıntılı PipelineVariable, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```