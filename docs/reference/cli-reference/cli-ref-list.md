---
title: NuGet CLı listesi komutu
description: NuGet. exe list komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328326"
---
# <a name="list-command-nuget-cli"></a>List komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi, yayımlama &bullet; **Desteklenen sürümler:** tümü

Belirli bir kaynaktaki paketlerin listesini görüntüler. Hiçbir kaynak belirtilmemişse, genel yapılandırma dosyasında `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config`' de tanımlanan tüm kaynaklar kullanılır. Kaynak belirtilmezse, varsayılan akışı kullanır (NuGet.org). `list` `NuGet.Config`

## <a name="usage"></a>Kullanım

```cli
nuget list [search terms] [options]
```

isteğe bağlı arama terimleri, görüntülenecek listeyi filtreleyecek. Arama terimleri, paketler, Etiketler ve paket açıklamaları adlarına, bunları nuget.org 'de kullanırken olduğu gibi uygulanır.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| AllVersions | Bir paketin tüm sürümlerini listeleyin. Varsayılan olarak, yalnızca en son paket sürümü görüntülenir. |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Help | Komut için yardım bilgilerini görüntüler. |
| IncludeDelisted | *(3.2 +)* Listelenmemiş paketleri görüntüle. |
| NonInteractive | Kullanıcı girişi veya onayları için istemleri bastırır. |
| PreRelease | Listedeki yayın öncesi paketleri içerir. |
| Source | Aranacak paket kaynaklarının bir listesini belirtir. |
| Verbosity | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
