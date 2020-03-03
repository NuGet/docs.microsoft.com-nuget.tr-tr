---
title: NuGet CLı setapikey komutu
description: NuGet. exe setapikey komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231233"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi, yayımlama &bullet; **Desteklenen sürümler:** tümü

Belirli bir sunucu URL 'SI için bir API anahtarını, sonraki komutlara girilmesi gerekmiyorsa, `NuGet.Config` ' a kaydeder.

## <a name="usage"></a>Kullanım

```cli
nuget setapikey <key> -Source <url> [options]
```

Burada `<source>` sunucuyu tanımlar ve `<key>` kaydedilecek anahtardır. `<source>` atlanırsa, nuget.org varsayılır. 

> [!NOTE]
> API anahtarı özel akışta kimlik doğrulaması için kullanılmaz. Kaynak ile kimlik doğrulaması için kimlik bilgilerini yönetmek üzere [`nuget sources` komutuna](../cli-reference/cli-ref-sources.md) bakın.
> Tek bir NuGet sunucusundan API anahtarları elde edilebilir. Nuget.org için APIKeys oluşturmak ve yönetmek için bkz. [Yayımla-api-Key](../../quickstart/includes/publish-api-key.md)

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Yardım | Komut için yardım bilgilerini görüntüler. |
| NonInteractive | Kullanıcı girişi veya onayları için istemleri bastırır. |
| Ayrıntı Düzeyi | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
