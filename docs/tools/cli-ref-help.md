---
title: NuGet CLI Yardım komutu
description: Nuget.exe Yardım komut başvurusu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d7112209a0a2a267343c3458ebacaf6b744786a9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818262"
---
# <a name="help-or--command-nuget-cli"></a>help or ? Komut (NuGet CLI)

**Uygulandığı öğe:** tüm &bullet; **desteklenen sürümleri**: tüm

Yardım bilgisi ve bilgi belirli komutlar hakkında Yardım genel görüntüler.

## <a name="usage"></a>Kullanım

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

Burada [komut] Yardım görüntülemek için belirli bir komutu belirtir.

> [!Warning]
> Bazı komutlar ile belirtmek dikkatli olmanızı *yardımcı* ilk olarak ile `nuget help install`, nuget.org üzerinde "Yardım" adlı bir paketi olduğundan. Komut verirseniz `nuget install help`, yükleme komutunda Yardım çalışmaz, ancak bunun yerine Yardım adlı paketi yükler.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| Tümü | Tüm kullanılabilir komutlar için ayrıntılı yardım yazdırma; belirli bir komut belirtilmezse yoksayıldı. |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi Yardım komutu için yardımı görüntüler. |
| Markdown | Ayrıntılı Yardımı ile kullanıldığında markdown biçimde yazdırma `-All`. Aksi halde yoksayılır. |
| NonInteractive | Kullanıcı girişi veya onayı için ister gizler. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
