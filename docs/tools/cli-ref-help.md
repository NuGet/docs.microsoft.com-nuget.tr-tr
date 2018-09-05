---
title: NuGet CLI Yardım komutu
description: Nuget.exe Yardım komut başvurusu
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546569"
---
# <a name="help-or--command-nuget-cli"></a>help or ? Komut (NuGet CLI)

**İçin geçerlidir:** tüm &bullet; **desteklenen sürümler**: tüm

Genel görüntüler, bilgi yardımcı olmak ve özel komutlar hakkında bilgi yardımcı olur.

## <a name="usage"></a>Kullanım

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

Burada [komut] Yardım görüntülemek istediğiniz belirli bir komutu belirtir.

> [!Warning]
> Bazı komutlarla belirtmek dikkatli olmanızı *yardımcı* ilk olarak ile `nuget help install`nuget.org adresinden "help" adlı bir paketi olduğundan. Komutunu verirseniz `nuget install help`, Yardım yükleme komutunu vermeyeceğiz ancak bunun yerine Yardım adlı paketi yükler.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| Tümü | Tüm kullanılabilir komutları için yazdırma ayrıntılı Yardım; belirli bir komut verildi yoksayılır. |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar. |
| Yardım | Bilgi Yardım komut için yardımı görüntüler. |
| Markdown | Ayrıntılı Yardımı ile kullanıldığında, markdown biçiminde yazdırma `-All`. Aksi halde yoksayılır. |
| NonInteractive | Kullanıcı girişini veya onaylar ister bastırır. |
| Ayrıntı Düzeyi | Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
