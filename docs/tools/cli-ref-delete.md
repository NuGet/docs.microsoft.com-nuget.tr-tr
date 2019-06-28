---
title: NuGet CLI delete komutu
description: Nuget.exe delete komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3ea2dc3e87d0a626704fe5623d39eaf5bd3f3446
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426115"
---
# <a name="delete-command-nuget-cli"></a>Sil komutu (NuGet CLI)

**İçin geçerlidir:** paket yayımlama &bullet; **desteklenen sürümler:** tüm

Bir paketi paket kaynağından unlists veya siler. Nuget.org, delete komutu için [paket unlists](../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Kullanım

```cli
nuget delete <packageID> <packageVersion> [options]
```

Burada `<packageID>` ve `<packageVersion>` silme veya listeden tam paket tanımlayın. Tam davranış kaynağa bağlıdır. Yerel klasörler için paketi örneği için silinir; nuget.org için listelenmemiş bir pakettir.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ApiKey | Hedef depo için API anahtarı. Yoksa, yapılandırma dosyasında belirtilen kullanılır. |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar. |
| Help | Bilgi komut için yardımı görüntüler. |
| NonInteractive | Kullanıcı girişini veya onaylar ister bastırır. |
| Source | Sunucu URL'sini belirtir. Nuget.org URL'si `https://api.nuget.org/v3/index.json`. Özel akışları için örneğin, ana bilgisayar adı yerine *%hostname%/api/v3*. |
| Verbosity | Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
