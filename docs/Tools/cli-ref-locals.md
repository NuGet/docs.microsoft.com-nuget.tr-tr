---
title: NuGet CLI Yereller komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe Yereller komut başvurusu"
keywords: "nuget Yereller başvuru, Yereller komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="locals-command-nuget-cli"></a>Yerel öğeler komutu (NuGet CLI)

**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** 3.3 +

Temizler veya http isteği önbelleği, paketleri önbellek ve makine genelinde genel paketler klasörü gibi yerel NuGet kaynakları listeler. `locals` Komut ayrıca konumların bir listesini görüntülemek için kullanılabilir. Daha fazla bilgi için bkz: [NuGet önbelleği yönetme](../consume-packages/managing-the-nuget-cache.md).

## <a name="usage"></a>Kullanım

```cli
nuget locals <cache> [options]
```

Burada `<cache>` biri `all`, `http-cache`, `packages-cache`, `global-packages`, ve `temp` *(3.4 +)*.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| Temizle | Belirtilen önbellek temizler. |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır. |
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| List | Belirtilen önbellek konumunu veya kullanıldığında tüm önbellekleri konumlarını listeler *tüm*. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget locals all -list
nuget locals http-cache -clear
```
