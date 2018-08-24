---
title: NuGet CLI Yereller komutu
description: Nuget.exe Yereller komut başvurusu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 38d8b9366fb2749b77c987c950da3aa9e7f029fc
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794141"
---
# <a name="locals-command-nuget-cli"></a>Yerel öğeler komut (NuGet CLI)

**İçin geçerlidir:** paketini tüketim &bullet; **desteklenen sürümler:** 3.3 +

Temizler veya yerel NuGet kaynakları gibi listeler *http önbellek*, *genel paketleri* klasör ve geçici klasör. `locals` Komutu ayrıca kullanılabilir konumların bir listesini görüntüleyin. Daha fazla bilgi için [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Kullanım

```cli
nuget locals <folder> [options]
```

Burada `<folder>` biri `all`, `http-cache`, `packages-cache` *(3.5 ve önceki)*, `global-packages`, `temp` *(3.4 ve üzeri)*, ve `plugins-cache` *(4.8 +)*.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| Temizle | Belirtilen klasör temizler. |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar. |
| Yardım | Bilgi komut için yardımı görüntüler. |
| List | Belirtilen klasör konumunu veya ile kullanıldığında tüm klasör konumlarını listeler *tüm*. |
| NonInteractive | Kullanıcı girişini veya onaylar ister bastırır. |
| Ayrıntı Düzeyi | Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Diğer örnekler için [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md).
