---
title: NuGet CLI Listele komutu
description: Nuget.exe Listele komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549807"
---
# <a name="list-command-nuget-cli"></a>Liste komut (NuGet CLI)

**İçin geçerlidir:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm

Paketlerin belirli bir kaynaktan bir listesini görüntüler. Kaynağı yok belirtilirse, genel yapılandırma dosyasında tanımlanan tüm kaynakları `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config`, kullanılır. Varsa `NuGet.Config` kaynağı yok, ardından belirtir `list` varsayılan akışı (nuget.org) kullanır.

## <a name="usage"></a>Kullanım

```cli
nuget list [search terms] [options]
```

İsteğe bağlı arama terimlerini görüntülenen listeyi filtrelemek burada. Bunları nuget.org adresinden kullanırken olduğu gibi arama terimlerini paketleri, etiketleri ve açıklamaları paket adları için uygulanır.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| AllVersions | Bir paketin tüm sürümlerini listeler. Varsayılan olarak, yalnızca en son Paket sürümü görüntülenir. |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar. |
| Yardım | Bilgi komut için yardımı görüntüler. |
| IncludeDelisted | *(3.2 +)*  Listelenmemiş paketleri görüntüler. |
| NonInteractive | Kullanıcı girişini veya onaylar ister bastırır. |
| Yayın öncesi | Yayın öncesi paketleri listesine ekler. |
| Kaynak | Aranacak paket kaynaklarını listesini belirtir. |
| Ayrıntı Düzeyi | Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
