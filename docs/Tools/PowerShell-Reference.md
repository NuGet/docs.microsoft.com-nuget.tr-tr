---
title: "NuGet PowerShell başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/2/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: cd08b869-44c6-480e-90f7-494a6d08e6d0
description: "Visual Studio'da NuGet Paket Yöneticisi konsolunda kullanılabilir PowerShell komutlarını tam referansı."
keywords: "NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0da5c88447784fdd49d824bbd03b11f73c22ebc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="powershell-reference"></a>PowerShell başvurusu

Paket Yöneticisi konsolu, bir PowerShell arabirimi belirli komutları NuGet ile etkileşim kurmak için Windows Visual Studio'dan aşağıda listelenen sağlar. (Konsol Mac için Visual Studio şu anda kullanılabilir değil) Konsolunu kullanarak için bir kılavuz için bkz: [Paket Yöneticisi Konsolu](../tools/package-manager-console.md) konu.

> [!Tip]
> Tüm PowerShell komutları yalnızca paket tüketimi ilgilidir. PowerShell komutlarını oluşturmak ve bir paket ayrıca diğer paketleri tüketicisi olarak toplasa bile dışında paketleri yayımlamak için ilgilidir.

> [!Important]
> Burada listelenen komutlar Visual Studio'da Paket Yöneticisi konsolu özgüdür ve farklı [paket Yönetimi Modülü komutları](https://msdn.microsoft.com/powershell/reference/6/packagemanagement/packagemanagement) genel bir PowerShell ortamında kullanılabilir. Özellikle, her bir ortamda, diğer kullanılabilir olmayan komutlar sahip ve aynı ada sahip komutları kendi belirli değişkenlerinde farklı olabilir. Visual Studio'da paket Yönetimi konsolunu kullanarak, komutları ve mevcut bu konudaki belgelenen bağımsız değişkenleri uygulanır.

| Sık kullanılan komutlar | Açıklama | NuGet sürümü |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | Bir paketi ve bağımlılıklarını projeye yükler. | Tümü |
| [Güncelleştirme paketi](ps-ref-update-package.md) | Bir paketi ve bağımlılıklarını veya projesindeki tüm paketleri güncelleştirir. | Tümü |
| [Paket Bul](ps-ref-find-package.md) | Bir paket kimliği veya anahtar sözcükleri kullanarak paket kaynağını arar. | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | Yerel depoda yüklü olan paketlerin listesini alır veya paket kaynağındaki paketleri listeler. | Tümü |

| İkincil komutları | Açıklama | NuGet sürümü |
| --- | --- | --- |
| [BindingRedirect ekleme](ps-ref-add-bindingredirect.md) | Bir proje için çıkış yolu içindeki tüm derlemelerde inceler ve bağlama yeniden yönlendirmelerini ekler `app.config` veya `web.config` gerektiğinde. | Tümü |
| [Get-proje](ps-ref-get-project.md) | Varsayılan ya da belirtilen proje hakkındaki bilgileri görüntüler. | 3.0+ |
| [Açık PackagePage](ps-ref-open-packagepage.md) | Proje, lisans veya belirtilen paket için rapor kötüye URL'si ile varsayılan tarayıcı başlatır. | 3.0 +'da kullanım dışıdır |
| [Register-TabExpansion](ps-ref-register-tabexpansion.md) | Bir sekme genişlemesi parametreler için yaygın olarak kullanılan parametre değerleri için özelleştirilmiş genişletmeleri oluşturmanızı sağlayan bir komut kaydeder. | Tümü |
| [Eşitleme paketi](ps-ref-sync-package.md) | Get paketinden yüklü sürümü proje belirtilen ve sürümü çözümdeki projelerin geri kalanına eşitlenir. | 3.0+ |
| [Kaldırma paketi](ps-ref-uninstall-package.md) | Bir paket bağımlılıklarını isteğe bağlı olarak kaldırarak bir projeden kaldırır. | Tümü |

Konsolu içinden aşağıdaki komutlardan birini ilgili eksiksiz, ayrıntılı yardım için yalnızca söz konusu komut adı ile aşağıdaki komutu çalıştırın:

```ps
Get-Help <command> -full
```

Tüm Paket Yöneticisi Konsolu komutları aşağıdaki desteği [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216):

- Hata ayıklama
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Ayrıntılı
- WarningAction
- WarningVariable

Ayrıntılar için başvurmak [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) PowerShell belgelerinde.
