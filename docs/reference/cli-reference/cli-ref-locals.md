---
title: NuGet CLı Yereller komutu
description: nuget.exe Yereller komutuna yönelik başvuru
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 25feb29c7b96c47681cedd8208b8595952d3ca49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779203"
---
# <a name="locals-command-nuget-cli"></a>Yereller komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** 3.3 +

*Http önbelleği*, *genel paketler* klasörü ve temp klasörü gibi yerel NuGet kaynaklarını temizler veya listeler. `locals`Komut ayrıca bu konumların bir listesini göstermek için de kullanılabilir. Daha fazla bilgi için bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

## <a name="usage"></a>Kullanım

```cli
nuget locals <folder> [options]
```

Burada `<folder>` `all` ,, `http-cache` , `packages-cache` *(3,5 ve öncesi)*, `global-packages` , `temp` *(3.4 +)* ve `plugins-cache` *(4.8 +)*' den biridir.

## <a name="options"></a>Seçenekler

- **`-Clear`**

  Belirtilen klasörü temizler.

- **`-ConfigFile`**

  Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.

- **`-ForceEnglishOutput`**

  *(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.

- **`-?|-help`**

  Komut için yardım bilgilerini görüntüler.

- **`-List`**

  Belirtilen klasörün konumunu veya tüm klasörlerin konumlarını, *Tümü* ile birlikte kullanıldığında listeler.

- **`-NonInteractive`**

  Kullanıcı girişi veya onayları için istemleri bastırır.

- **`-Verbosity [normal|quiet|detailed]`**

  Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget locals all -list
nuget locals http-cache -clear
```

Daha fazla örnek için bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md).
