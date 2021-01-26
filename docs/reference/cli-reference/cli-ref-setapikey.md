---
title: NuGet CLı setapikey komutu
description: nuget.exe setapikey komutuna yönelik başvuru
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3e0c2f84e336e0a642b1b5e815e74a1fb0878467
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780016"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi, yayımlama &bullet; **Desteklenen sürümler:** tümü

Belirli bir sunucu URL 'SI için bir API anahtarını `NuGet.Config` , sonraki komutlara girilmesi gerekmemesi için öğesine kaydeder.

## <a name="usage"></a>Kullanım

```cli
nuget setapikey <key> -Source <url> [options]
```

Burada `<source>` sunucuyu tanımlar ve `<key>` kaydedilecek anahtardır. `<source>`Atlanırsa, NuGet.org varsayılır. 

> [!NOTE]
> API anahtarı özel akışta kimlik doğrulaması için kullanılmaz. Kaynak ile kimlik doğrulaması için kimlik bilgilerini yönetmek üzere [ `nuget sources` komutuna](../cli-reference/cli-ref-sources.md) bakın.
> Tek bir NuGet sunucusundan API anahtarları elde edilebilir. Nuget.org için APIKeys oluşturmak ve yönetmek için- [api-Key alma](../../nuget-org/scoped-api-keys.md#acquire-an-api-key) bölümüne bakın

## <a name="options"></a>Seçenekler

- **`-ConfigFile`**

  Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.

- **`-ForceEnglishOutput`**

  *(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.

- **`-?|-help`**

  Komut için yardım bilgilerini görüntüler.

- **`-NonInteractive`**

  Kullanıcı girişi veya onayları için istemleri bastırır.

- **`-src|-Source`**

  API anahtarının geçerli olduğu sunucu URL 'SI.

- **`-Verbosity [normal|quiet|detailed]`**

  Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
