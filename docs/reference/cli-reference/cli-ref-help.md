---
title: NuGet CLı yardım komutu
description: NuGet. exe yardım komutu başvurusu
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328344"
---
# <a name="help-or--command-nuget-cli"></a>help or ? komut (NuGet CLı)

**Uygulama hedefi:** &bullet; tüm **Desteklenen sürümler**: tümü

Belirli komutlarla ilgili genel yardım bilgilerini ve yardım bilgilerini görüntüler.

## <a name="usage"></a>Kullanım

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

Burada [komut], yardım görüntülenecek belirli bir komutu tanımlar.

> [!Warning]
> Bazı komutlarla, NuGet.org üzerinde "Help" adlı bir  paket olduğu için, `nuget help install`' da olduğu gibi öncelikle yardım 'ı belirtmek için küçük bir değer belirleyin. Komuta `nuget install help`sahipseniz, install komutuyla ilgili yardım almaz, ancak bunun yerine yardım adlı paketi yükleyeceksiniz.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| Tümü | Tüm kullanılabilir komutlar için ayrıntılı yardım Yazdır; belirli bir komut verildiyse yoksayıldı. |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Help | Yardım komutunun kendisi için yardım bilgilerini görüntüler. |
| Markdown | İle `-All`kullanıldığında markaşağı biçiminde ayrıntılı yardım yazdırın. Aksi halde yoksayıldı. |
| NonInteractive | Kullanıcı girişi veya onayları için istemleri bastırır. |
| Verbosity | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
