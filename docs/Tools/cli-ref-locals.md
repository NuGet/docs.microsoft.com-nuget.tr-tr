---
title: NuGet CLI Yereller komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe Yereller komut başvurusu
keywords: nuget Yereller başvuru, Yereller komutu
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0122c79e55b12838bd123cf91bfcbc5dbbd2a65c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
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
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Ek örnekler için bkz: [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md).
