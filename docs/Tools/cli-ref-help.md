---
title: NuGet CLI Yardım komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe Yardım komut başvurusu
keywords: nuget Yardım başvurusu, Yardım komutu
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 440861e53b4a9ff73a9d3e8a2a3dad7dbddc9584
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="help-or--command-nuget-cli"></a>Yardım veya? Komut (NuGet CLI)

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
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
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
