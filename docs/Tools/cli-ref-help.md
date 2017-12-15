---
title: "NuGet CLI Yardım komutu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 780d7f52-d6c6-45cd-8a62-218ff8c0b270
description: "Nuget.exe Yardım komut başvurusu"
keywords: "nuget Yardım başvurusu, Yardım komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 55dc263fedd7ed5a3e48b76dbc9a3ccc220655cf
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="help-or--command-nuget-cli"></a>Yardım veya? Komut (NuGet CLI)

**Uygulandığı öğe:** tüm &bullet; **desteklenen sürümleri**: tüm

Yardım bilgisi ve bilgi belirli komutlar hakkında Yardım genel görüntüler.

## <a name="usage"></a>Kullanım

```
nuget help [command] [options]
nuget ? [command] [options]
```

Burada [komut] Yardım görüntülemek için belirli bir komutu belirtir.

> [!Warning]
> Bazı komutlar ile belirtmek dikkatli olmanızı *yardımcı* ilk olarak ile `nuget help install`, nuget.org üzerinde "Yardım" adlı bir paketi olduğundan. Komut verirseniz `nuget install help`, Yardım yükleme komutunda alırsınız değil, ancak bunun yerine Yardım adlı paketi yükler.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| Tümü | Tüm kullanılabilir komutlar için ayrıntılı yardım yazdırma; belirli bir komut belirtilmezse yoksayıldı. |
| ConfigFile | *(2.5 +)*  Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır. |
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi Yardım komutu için yardımı görüntüler. |
| Markdown | Ayrıntılı Yardımı ile kullanıldığında markdown biçimde yazdırma `-All`. Aksi halde yoksayılır. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *(2.5 +) ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
