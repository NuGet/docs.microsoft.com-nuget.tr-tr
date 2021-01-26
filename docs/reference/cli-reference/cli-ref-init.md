---
title: NuGet CLı init komutu
description: nuget.exe Init komutu başvurusu
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f37572624cea744ce60a9a2e58ad3cbe2696cb9e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780075"
---
# <a name="init-command-nuget-cli"></a>init komutu (NuGet CLı)

**Uygulama hedefi:** paket oluşturma &bullet; **Desteklenen sürümler:** 3.3 +

Bir düz klasörden tüm paketleri, [Add komutunda](cli-ref-add.md)açıklandığı gibi hiyerarşik bir düzen kullanarak bir hedef klasöre kopyalar. Diğer bir deyişle, bu, `init` `add` klasöründeki her pakette komutunu kullanmakla eşdeğerdir.

İle olduğu gibi `add` , hedef yerel bir klasör ya da bır UNC yolu olmalıdır; Nuget.org veya özel sunucular gibi HTTP paket depoları desteklenmez.

## <a name="usage"></a>Kullanım

```cli
nuget init <source> <destination> [options]
```

, `<source>` paketleri içeren klasördür ve `<destination>` paketlerin kopyalandığı yerel klasör veya UNC yol adı olur.

## <a name="options"></a>Seçenekler

- **`-ConfigFile`**

  Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.

- **`-Expand`**

  Paket kaynağına eklenen her pakette bulunan tüm dosyaları ekler; komutuyla aynı `-Expand` `add` .

- **`-ForceEnglishOutput`**

  *(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.

- **`-?|-help`**

  Komut için yardım bilgilerini görüntüler.

- **`-NonInteractive`**

  Kullanıcı girişi veya onayları için istemleri bastırır.

- **`-Verbosity [normal|quiet|detailed]`**

  Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
