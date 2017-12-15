---
title: NuGet CLI Yereller komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 7f672c7c-74c9-4296-bc27-4d47882b541c
description: "Nuget.exe Yereller komut başvurusu"
keywords: "nuget Yereller başvuru, Yereller komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8cc06eedc20507e2bdd210e40c471ff551b89563
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
## <a name="locals-command-nuget-cli"></a>Yerel öğeler komutu (NuGet CLI)

**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** 3.3 +

Temizler veya http isteği önbelleği, paketleri önbellek ve makine genelinde genel paketler klasörü gibi yerel NuGet kaynakları listeler. `locals` Komut ayrıca konumların bir listesini görüntülemek için kullanılabilir. Daha fazla bilgi için bkz: [NuGet önbelleği yönetme](../consume-packages/managing-the-nuget-cache.md).

## <a name="usage"></a>Kullanım

```
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

```
nuget locals all -list
nuget locals http-cache -clear
```
