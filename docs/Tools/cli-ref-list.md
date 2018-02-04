---
title: NuGet CLI Listele komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Başvuru için nuget.exe Listele komutu"
keywords: "nuget listesi başvurusu, liste paketleri komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5a1f68aaffd26a0f903aa3a7a4a450a0121191c3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="list-command-nuget-cli"></a>LIST komutu (NuGet CLI)

**Uygulandığı öğe:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm

Belirli bir kaynaktan alınan paketlerin listesini görüntüler. Herhangi bir kaynağa belirtilirse, genel yapılandırma dosyasında tanımlanmış tüm kaynakları `%AppData%\NuGet\NuGet.Config`, kullanılır. Varsa `NuGet.Config` herhangi bir kaynağa sonra belirtir `list` varsayılan akışı (nuget.org) kullanır.

## <a name="usage"></a>Kullanım

```cli
nuget list [search terms] [options]
```

Burada isteğe bağlı arama terimleri görüntülenen listeyi filtrelemek. Arama terimleri paketler, etiketler ve paket açıklamaları adlarını uygulanır.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| AllVersions | Bir paketin tüm sürümleri listelenir. Varsayılan olarak, yalnızca son Paket sürümü görüntülenir. |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır. |
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| IncludeDelisted | *(3.2 +)*  Listelenmemiş paketleri görüntüler. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Yayın öncesi | Ön sürüm paketlerini listede içerir. |
| Kaynak | Aranacak paket kaynaklarının listesini belirtir. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget list

nuget list -Verbosity detailed -AllVersions
```
