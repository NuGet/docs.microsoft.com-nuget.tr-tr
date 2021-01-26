---
title: NuGet CLı yardım komutu
description: nuget.exe Help komutuna yönelik başvuru
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5d91638c4a6f167ea8a04e5dfa2905cb55084ddd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779361"
---
# <a name="help-or--command-nuget-cli"></a>help or ? komut (NuGet CLı)

**Uygulama hedefi:** tüm &bullet; **Desteklenen sürümler**: tümü

Belirli komutlarla ilgili genel yardım bilgilerini ve yardım bilgilerini görüntüler.

## <a name="usage"></a>Kullanım

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

Burada [komut], yardım görüntülenecek belirli bir komutu tanımlar.

> [!Warning]
> Bazı komutlarla,  `nuget help install` NuGet.org üzerinde "Help" adlı bir paket olduğu için, ' da olduğu gibi öncelikle yardım 'ı belirtmek için küçük bir değer belirleyin. Komuta sahipseniz `nuget install help` , install komutuyla ilgili yardım almaz, ancak bunun yerine yardım adlı paketi yükleyeceksiniz.

## <a name="options"></a>Seçenekler

- **`-All`**

  Tüm kullanılabilir komutlar için ayrıntılı yardım Yazdır; belirli bir komut verildiyse yoksayıldı.

- **`-ConfigFile`**

  Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.

- **`-ForceEnglishOutput`**

  *(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.

- **`-?|-help`**

  Komut için yardım bilgilerini görüntüler.

- **`-Markdown`**

  İle kullanıldığında markaşağı biçiminde ayrıntılı yardım yazdırın `-All` . Aksi halde yoksayıldı.

- **`-NonInteractive`**

  Kullanıcı girişi veya onayları için istemleri bastırır.

- **`-Verbosity [normal|quiet|detailed]`**

  Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
