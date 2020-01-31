---
title: NuGet CLı listesi komutu
description: NuGet. exe list komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813344"
---
# <a name="list-command-nuget-cli"></a>List komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi, yayımlama &bullet; **Desteklenen sürümler:** tümü

Belirli bir kaynaktaki paketlerin listesini görüntüler. Hiçbir kaynak belirtilmemişse, genel yapılandırma dosyasında tanımlanan tüm kaynaklar `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config`kullanılır. `NuGet.Config` kaynak belirtiyorsa `list` varsayılan akışı kullanır (nuget.org).

## <a name="usage"></a>Kullanım

```cli
nuget list [search terms] [options]
```

isteğe bağlı arama terimleri, görüntülenecek listeyi filtreleyecek. Arama terimleri, paketler, Etiketler ve paket açıklamaları adlarına, bunları nuget.org 'de kullanırken olduğu gibi uygulanır.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| AllVersions | Bir paketin tüm sürümlerini listeleyin. Varsayılan olarak, yalnızca en son paket sürümü görüntülenir. |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Yardım | Komut için yardım bilgilerini görüntüler. |
| IncludeDelisted | *(3.2 +)* Listelenmemiş paketleri görüntüle. |
| NonInteractive | Kullanıcı girişi veya onayları için istemleri bastırır. |
| PreRelease | Listedeki yayın öncesi paketleri içerir. |
| Kaynak | Aranacak paket kaynaklarının bir listesini belirtir. |
| Ayrıntı Düzeyi | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

Yapılandırılmış akışlardan tüm paketleri Listele:
```
nuget list
```
Ayrıntılı ayrıntı düzeyine sahip Azure ile ilgili paketleri listeleyin:
```
nuget list Azure -Verbosity detailed
```
Yapılandırılmış akışlardan Azure ile ilgili paketlerin tüm sürümlerini listeleyin:
```
nuget list Azure -AllVersions
```
JSON ile ilgili tüm paketlerin sürümlerini belirtilen kaynaktan/akıştan listeleyin:
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
Birden çok kaynaktan/akışlardan JSON ile ilgili paketleri Listele:
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

