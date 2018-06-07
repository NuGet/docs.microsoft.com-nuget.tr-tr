---
title: NuGet CLI delete komutu
description: Nuget.exe delete komutu için başvurusu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0f33dd5475521da47972a6f032ac6ea86d98c83
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817184"
---
# <a name="delete-command-nuget-cli"></a>delete komutu (NuGet CLI)

**Uygulandığı öğe:** paketini yayımlama &bullet; **desteklenen sürümler:** tüm

Bir paketi paket kaynağında unlists veya siler. Nuget.org, delete komutu için [paket unlists](../policies/deleting-packages.md).

## <a name="usage"></a>Kullanım

```cli
nuget delete <packageID> <packageVersion> [options]
```

Burada `<packageID>` ve `<packageVersion>` unlist veya silmek için tam paketi belirleyin. Tam davranışı kaynağa bağlıdır. Yerel klasör için örneğin, paket silindi; nuget.org için listelenmeyen paketidir.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| apikey ile yapılan | Hedef depo API anahtarı. Yoksa, yapılandırma dosyasında belirtilen bir kullanılır. |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| NonInteractive | Kullanıcı girişi veya onayı için ister gizler. |
| Kaynak | Sunucu URL'sini belirtir. Nuget.org URL'si `https://api.nuget.org/v3/index.json`. Örneğin, özel akışları için ana bilgisayar adı yerine *%hostname%/api/v3*. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
