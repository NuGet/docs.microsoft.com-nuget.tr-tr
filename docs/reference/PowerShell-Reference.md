---
title: NuGet PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolunda bulunan PowerShell komutlarına yönelik tüm başvuru.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 142af9c4f7d25c3b0d986524313851cceb1e4c60
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328383"
---
# <a name="powershell-reference"></a>PowerShell başvurusu

Paket Yöneticisi konsolu, Windows üzerinde Visual Studio 'da aşağıda listelenen belirli komutlarla NuGet ile etkileşim kurmak için bir PowerShell arabirimi sağlar. (Konsol Mac için Visual Studio ' de şu anda kullanılabilir değil.) Konsolunu kullanma kılavuzu için bkz. [Paket Yöneticisi konsolu kullanılarak paketleri yükleyip yönetme](../consume-packages/install-use-packages-powershell.md) konusu.

> [!Tip]
> Tüm PowerShell komutları yalnızca paket tüketimiyle ilgilidir. Bir paketin başka paketlerin bir tüketicisi de olması dışında, paket oluşturma ve yayımlama ile ilgili bir PowerShell komutu yoktur.

> [!Important]
> Burada listelenen komutlar, Visual Studio 'da Paket Yöneticisi konsoluna özgüdür ve genel bir PowerShell ortamında kullanılabilir olan [paket yönetimi modülü komutlarından](/powershell/module/packagemanagement/?view=powershell-6) farklıdır. Özellikle, her ortamın diğeri üzerinde kullanılamayan komutları vardır ve aynı ada sahip komutlar, belirli bağımsız değişkenlerinde de farklılık gösterebilir. Visual Studio 'da Paket Yönetimi konsolunu kullanırken, bu konu başlığı altında belgelenen komutlar ve bağımsız değişkenler geçerlidir.

| Ortak komutlar | Açıklama | NuGet sürümü |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | Bir paketi ve onun bağımlılıklarını projeye kurar. | Tümü |
| [Update-Package](ps-reference/ps-ref-update-package.md) | Bir paketi ve onun bağımlılıklarını veya bir projedeki tüm paketleri güncelleştirir. | Tümü |
| [Find-Package](ps-reference/ps-ref-find-package.md) | Paket KIMLIĞINI veya anahtar sözcüklerini kullanarak bir paket kaynağını arar. | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | Yerel depoda yüklü paketlerin listesini alır veya bir paket kaynağından kullanılabilir paketleri listeler. | Tümü |

| İkincil komutlar | Açıklama | NuGet sürümü |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | Bir projenin çıkış yolundaki tüm derlemeleri inceler ve ' a `app.config` veya `web.config` gerektiğinde bağlama yeniden yönlendirmeleri ekler. | Tümü |
| [Get-Project](ps-reference/ps-ref-get-project.md) | Varsayılan veya belirtilen proje hakkındaki bilgileri görüntüler. | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | Belirtilen paket için proje, lisans veya uygunsuz kullanım URL 'SI ile varsayılan tarayıcıyı başlatır. | 3\.0 + ' da kullanım dışı |
| [Register-Tabgenişleme](ps-reference/ps-ref-register-tabexpansion.md) | Bir komutun parametreleri için bir sekme genişletmesi kaydeder, bu da yaygın olarak kullanılan parametre değerleri için özelleştirilmiş expanlar oluşturmanıza olanak sağlar. | Tümü |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | Belirtilen projeden yüklü paketin sürümünü alın ve sürümü çözümdeki diğer projelere eşitler. | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | , İsteğe bağlı olarak bağımlılıklarını kaldırarak bir projeden paket kaldırır. | Tümü |

Konsolun içindeki bu komutlardan herhangi biri hakkında ayrıntılı yardım için, aşağıdaki komut adı ile aşağıdakileri çalıştırmanız yeterlidir:

```ps
Get-Help <command> -full
```

Tüm Paket Yöneticisi konsol komutları aşağıdaki [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216)destekler:

- Hata ayıklama
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Ayrıntılı
- WarningAction
- WarningVariable

Ayrıntılar için PowerShell belgelerindeki [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) adresine bakın.
