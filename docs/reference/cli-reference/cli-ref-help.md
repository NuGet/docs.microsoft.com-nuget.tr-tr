---
title: NuGet CLı yardım komutu
description: nuget.exe Help komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 12776b7c16aeef223a0b682ee2468edec8ea3295
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623116"
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
> Bazı komutlarla, *help* `nuget help install` NuGet.org üzerinde "Help" adlı bir paket olduğu için, ' da olduğu gibi öncelikle yardım 'ı belirtmek için küçük bir değer belirleyin. Komuta sahipseniz `nuget install help` , install komutuyla ilgili yardım almaz, ancak bunun yerine yardım adlı paketi yükleyeceksiniz.

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
