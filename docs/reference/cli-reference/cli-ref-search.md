---
title: NuGet CLı arama komutu
description: nuget.exe Search komutu için başvuru
author: advay26
ms.author: t-adtand
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 35e4906960534299418cb2a17c190476708b2634
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623271"
---
# <a name="search-command-nuget-cli"></a>Search komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** 5,8 +

Sağlanan sorgu dizesini kullanarak belirli bir kaynağı arar. Kaynak belirtilmemişse,% AppData% \NuGet\NuGet.config içinde tanımlanan tüm kaynaklar kullanılır.

## <a name="usage"></a>Kullanım

```cli
nuget search [search terms] [options]
```

arama koşullarının, paketler, Etiketler ve paket açıklamaları adına, bunları nuget.org 'de kullanırken oldukları gibi, bu adlara uygulandığı yer.

## <a name="options"></a>Seçenekler

| Ad | Açıklama | Kullanım |
| ---  |     ---     |  :-:  |
| Sp1'in | Yayın öncesi paketleri varsayılan olarak dahil edilmez, ancak bu bağımsız değişken kullanılarak eklenebilir | -Ön sürüm |
| Kaynak | __nuget.config__ varsayılan kaynakları sorgulamak yerine aranacak belirli paket kaynakları | -Kaynak `<Source URL>`|
| Take | Döndürülecek sonuç sayısı. Varsayılan değer 20 ' dir. | -Al `<positive integer>` |
| Ayrıntı Düzeyi | Çıktıda görüntülenecek ayrıntı düzeyi. Varsayılan değer _normaldir_. (Aşağıdaki nota bakın)  | -Ayrıntı düzeyi `<quiet\|normal\|detailed>` |
| Yardım | Komut için yardım bilgilerini görüntüler | -Yardım |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

__NOT__

Ayrıntı düzeyleri:

* _sessiz_ paket kimliği, sürüm
* _normal_ -paket kimliği, sürüm, Indirmeler, açıklama önizlemesi
* _ayrıntılı_ -paket kimliği, sürüm, Indirmeler, tam açıklama, sorgu URL 'Si gibi diğer bilgiler

## <a name="examples"></a>Örnekler

Varsayılan kaynaklardan *günlüğe kaydetme*ile ilgili paketleri arayın:
```
nuget search logging
```
Ayrıntılı ayrıntı içeren *günlük*ile ilgili paketleri arayın:
```
nuget search logging -Verbosity detailed
```
*Günlüğe kaydetme*ile ilgili paketleri arayın ve yalnızca ilk 5 sonucu göster:
```
nuget search logging -Take 5
```
Yayın öncesi sürümleri de dahil olmak üzere, belirtilen kaynaktan/akıştan *JSON*ile ilgili paketleri arayın:
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
Birden çok kaynaktan/akışlardan *JSON*ile ilgili paketleri arayın:
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
