---
title: NuGet CLI Listele komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: "Başvuru için nuget.exe Listele komutu"
keywords: "nuget listesi başvurusu, liste paketleri komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a>LIST komutu (NuGet CLI)

**Uygulandığı öğe:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm

Belirli bir kaynaktan alınan paketlerin listesini görüntüler. Herhangi bir kaynağa belirtilirse, genel yapılandırma dosyasında tanımlanmış tüm kaynakları `%AppData%\NuGet\NuGet.Config`, kullanılır. Varsa `NuGet.Config` herhangi bir kaynağa sonra belirtir `list` varsayılan akışı (nuget.org) kullanır.

## <a name="usage"></a>Kullanım

```
nuget list [search terms] [options]
```

Burada isteğe bağlı arama terimleri görüntülenen listeyi filtrelemek. Arama terimleri paketler, etiketler ve paket açıklamaları adlarını uygulanır.

## <a name="options"></a>Seçenekler
| Seçenek | Açıklama |
| --- | --- |
| AllVersions | Bir paketin tüm sürümleri listelenir. Varsayılan olarak, yalnızca son Paket sürümü görüntülenir. |
| ConfigFile | *(2.5 +)*  Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır. |
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| IncludeDelisted | *(3.2 +)*  Listelenmemiş paketleri görüntüler. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Yayın öncesi | Ön sürüm paketlerini listede içerir. |
| Kaynak | Aranacak paket kaynaklarının listesini belirtir. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *(2.5 +) ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
