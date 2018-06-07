---
title: NuGet CLI Listele komutu
description: Başvuru için nuget.exe Listele komutu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b0f144d8abbba7388fe39cd113e4eeddccbca2c6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818444"
---
# <a name="list-command-nuget-cli"></a>LIST komutu (NuGet CLI)

**Uygulandığı öğe:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm

Belirli bir kaynaktan alınan paketlerin listesini görüntüler. Herhangi bir kaynağa belirtilirse, genel yapılandırma dosyasında tanımlanmış tüm kaynakları `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config`, kullanılır. Varsa `NuGet.Config` herhangi bir kaynağa sonra belirtir `list` varsayılan akışı (nuget.org) kullanır.

## <a name="usage"></a>Kullanım

```cli
nuget list [search terms] [options]
```

Burada isteğe bağlı arama terimleri görüntülenen listeyi filtrelemek. Nuget.org üzerinde kullanırken, olduğu gibi arama terimlerini paketler, etiketler ve paket açıklamaları adlarını uygulanır.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| AllVersions | Bir paketin tüm sürümleri listelenir. Varsayılan olarak, yalnızca son Paket sürümü görüntülenir. |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| IncludeDelisted | *(3.2 +)*  Listelenmemiş paketleri görüntüler. |
| NonInteractive | Kullanıcı girişi veya onayı için ister gizler. |
| Yayın öncesi | Ön sürüm paketlerini listede içerir. |
| Kaynak | Aranacak paket kaynaklarının listesini belirtir. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
