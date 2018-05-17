---
title: NuGet CLI Yereller komutu
description: Nuget.exe Yereller komut başvurusu
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ac07dc306bc23c2fedd33c5627e8d34a6098387c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="locals-command-nuget-cli"></a>locals komutu (NuGet CLI)

**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** 3.3 +

Temizler veya yerel NuGet kaynaklar gibi listeler *http önbellek*, *paketleri genel* klasörü ve geçici klasör. `locals` Komut ayrıca konumların bir listesini görüntülemek için kullanılabilir. Daha fazla bilgi için bkz: [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Kullanım

```cli
nuget locals <folder> [options]
```

Burada `<folder>` biri `all`, `http-cache`, `packages-cache` *(3.5 ve önceki)*, `global-packages`, ve `temp` *(3.4 +)*.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| Temizle | Belirtilen klasör temizler. |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| List | Belirtilen klasör konumunu veya kullanıldığında tüm klasör konumlarını listeler *tüm*. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Ek örnekler için bkz: [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md).
