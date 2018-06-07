---
title: NuGet CLI Yereller komutu
description: Nuget.exe Yereller komut başvurusu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818207"
---
# <a name="locals-command-nuget-cli"></a>Yerel öğeler komutu (NuGet CLI)

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
| NonInteractive | Kullanıcı girişi veya onayı için ister gizler. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Ek örnekler için bkz: [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md).
