---
title: NuGet CLı listesi komutu
description: nuget.exe list komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 91886dbbdcdb24648289d6f6efbe1f87e4099fff
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623077"
---
# <a name="list-command-nuget-cli"></a>List komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi, yayımlama &bullet; **Desteklenen sürümler:** tümü

Belirli bir kaynaktaki paketlerin listesini görüntüler. Hiçbir kaynak belirtilmemişse, genel yapılandırma dosyasında `%AppData%\NuGet\NuGet.Config` (Windows) veya ' de tanımlanan tüm kaynaklar `~/.nuget/NuGet/NuGet.Config` kullanılır. `NuGet.Config`Kaynak belirtilmezse, `list` varsayılan akışı kullanır (NuGet.org).

## <a name="usage"></a>Kullanım

```cli
nuget list [search terms] [options]
```

isteğe bağlı arama terimleri, görüntülenecek listeyi filtreleyecek. [Arama terimleri](/nuget/consume-packages/finding-and-choosing-packages#search-syntax) , paketler, Etiketler ve paket açıklamaları adlarına, bunları NuGet.org 'de kullanırken olduğu gibi uygulanır. 

## <a name="options"></a>Seçenekler

- **`-AllVersions`**

  Bir paketin tüm sürümlerini listeleyin. Varsayılan olarak, yalnızca en son paket sürümü görüntülenir.

- **`-ConfigFile`**

  Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.

- **`-ForceEnglishOutput`**

  *(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.

- **`-?|-help`**

  Komut için yardım bilgilerini görüntüler.

- **`-IncludeDelisted`**

  *(3.2 +)* Listelenmemiş paketleri görüntüle.

- **`-NonInteractive`**

  Kullanıcı girişi veya onayları için istemleri bastırır.

- **`-PreRelease`**

  Listedeki yayın öncesi paketleri içerir.

- **`-Source`**

  Aranacak paket kaynaklarının bir listesini belirtir.

- **`-Verbosity [normal|quiet|detailed]`**

  Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .

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
