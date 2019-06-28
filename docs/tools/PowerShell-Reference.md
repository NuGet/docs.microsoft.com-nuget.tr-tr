---
title: NuGet PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda kullanılabilir PowerShell komutlarının tam başvuru.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 977e06d36962366abd69f1c7f21ef33eca4e5029
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426119"
---
# <a name="powershell-reference"></a>PowerShell başvurusu

Paket Yöneticisi konsolu, bir PowerShell arabirimi belirli komutları NuGet ile etkileşim kurmak için Windows üzerinde Visual Studio içinde aşağıda listelenen sağlar. (Konsol, Mac için Visual Studio şu anda kullanılabilir değil) Konsolunu kullanarak bir kılavuz için bkz [yükleyin ve PowerShell kullanarak paketleri yönetme](../tools/package-manager-console.md) konu.

> [!Tip]
> Tüm PowerShell komutları yalnızca paket tüketimi ilgilidir. Herhangi bir PowerShell komut oluşturma ve bir paket diğer paketlerin bir tüketici de olabilir için toplasa bile, dışında paketleri yayımlama ilgilidir.

> [!Important]
> Burada listelenen komutlar, Visual Studio'da Paket Yöneticisi konsolu özgüdür ve farklı [paket Yönetimi Modülü komutları](/powershell/module/packagemanagement/?view=powershell-6) genel bir PowerShell ortamında kullanılabilir. Özellikle, her ortamın, diğer kullanılabilir olmayan komutları vardır ve aynı ada sahip komutları Ayrıca kendi özel bağımsız değişkenlerinde farklı. Visual Studio'da paket Yönetimi konsolunu kullanarak, komut ve bağımsız değişkenler mevcut Bu konu başlığında belirtildiği uygulayın.

| Sık kullanılan komutlar | Açıklama | NuGet Version |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | Projeye bir paketi ve bağımlılıkları yükler. | Tümü |
| [Update-Package](ps-ref-update-package.md) | Bir paketi ve bağımlılıkları veya bir projedeki tüm paketleri güncelleştirir. | Tümü |
| [Find-Package](ps-ref-find-package.md) | Bir paket kimliği veya anahtar sözcükleri kullanarak bir paket kaynağı arar. | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | Yerel depoda yüklü paketler listesini alır veya bir paket kaynağından paketleri listeler. | Tümü |

| İkincil komutları | Açıklama | NuGet Version |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | Çıkış yolu için bir proje içindeki tüm derlemeleri inceler ve ekler için bağlama yeniden yönlendirmeleri `app.config` veya `web.config` gerektiğinde. | Tümü |
| [Get-Project](ps-ref-get-project.md) | Varsayılan veya belirtilen proje hakkında bilgileri görüntüler. | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | Proje, lisans veya rapor Uygunsuz kullanım bildirme URL'si belirtilen paket için varsayılan tarayıcıda başlatır. | 3\.0 +'da kullanım dışı |
| [Register-TabExpansion](ps-ref-register-tabexpansion.md) | Sık kullanılan parametre değerleri için özelleştirilmiş genişletmeleri oluşturmanızı sağlayan bir komutunun parametreleri için bir sekme genişletmeyi kaydeder. | Tümü |
| [Sync-Package](ps-ref-sync-package.md) | Paket sürümü yüklü get proje belirtilen ve çözümdeki projelerin geri kalanı sürümüne eşitler. | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | Bir paket bağımlılıklarını isteğe bağlı olarak kaldırarak bir projeden kaldırır. | Tümü |

Yalnızca tam, ayrıntılı hakkında Yardım almak için konsol içinden bu komutlardan herhangi birine, söz konusu komut adı ile aşağıdaki komutu çalıştırın:

```ps
Get-Help <command> -full
```

Aşağıdaki tüm Paket Yöneticisi Konsolu komutları desteği [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216):

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
