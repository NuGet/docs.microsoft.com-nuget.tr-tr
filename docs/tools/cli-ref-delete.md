---
title: NuGet CLI delete komutu
description: Nuget.exe delete komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 11eea6e806d7bfe364587db9c7ef8374da1819f9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548516"
---
# <a name="delete-command-nuget-cli"></a>Sil komutu (NuGet CLI)

**İçin geçerlidir:** paket yayımlama &bullet; **desteklenen sürümler:** tüm

Bir paketi paket kaynağından unlists veya siler. Nuget.org, delete komutu için [paket unlists](../policies/deleting-packages.md).

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
