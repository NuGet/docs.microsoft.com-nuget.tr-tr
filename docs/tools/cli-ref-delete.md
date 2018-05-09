---
title: NuGet CLI delete komutu
description: Nuget.exe delete komutu için başvurusu
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 1db00a32d777f1c0247f855bf57a0dcf1c6734ae
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
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
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Kaynak | Sunucu URL'sini belirtir. Nuget.org URL'si `https://api.nuget.org/v3/index.json`. Örneğin, özel akışları için ana bilgisayar adı yerine *%hostname%/api/v3*. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```