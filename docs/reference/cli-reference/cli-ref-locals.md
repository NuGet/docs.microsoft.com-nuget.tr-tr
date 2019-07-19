---
title: NuGet CLı Yereller komutu
description: NuGet. exe Yereller komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328347"
---
# <a name="locals-command-nuget-cli"></a>Yereller komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** 3.3+

*Http önbelleği*, *genel paketler* klasörü ve temp klasörü gibi yerel NuGet kaynaklarını temizler veya listeler. `locals` Komut ayrıca bu konumların bir listesini göstermek için de kullanılabilir. Daha fazla bilgi için bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Kullanım

```cli
nuget locals <folder> [options]
```

Burada `<folder>` `all` `global-packages` `plugins-cache` , ,,`packages-cache` *(3,5 ve öncesi)* ,, `temp` *(3.4 +)* ve *(4.8 +)* ' den biridir. `http-cache`

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| Temizle | Belirtilen klasörü temizler. |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Help | Komut için yardım bilgilerini görüntüler. |
| List | Belirtilen klasörün konumunu veya tüm klasörlerin konumlarını, *Tümü*ile birlikte kullanıldığında listeler. |
| NonInteractive | Kullanıcı girişi veya onayları için istemleri bastırır. |
| Verbosity | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Daha fazla örnek için bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md).
