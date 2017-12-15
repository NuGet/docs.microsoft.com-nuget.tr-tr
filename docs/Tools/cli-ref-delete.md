---
title: NuGet CLI Sil komut | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: c213a07a-711d-47e0-9ee6-1d582e6cdb69
description: "Nuget.exe delete komutu için başvurusu"
keywords: "nuget başvuru, paketi komutu Sil"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 92af9dc356f3932347864976496e0ba1216496c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="delete-command-nuget-cli"></a>delete komutu (NuGet CLI)

**Uygulandığı öğe:** paketini yayımlama &bullet; **desteklenen sürümler:** tüm

Bir paketi paket kaynağında unlists veya siler. Nuget.org, delete komutu için [paket unlists](../policies/Deleting-Packages.md).

## <a name="usage"></a>Kullanım

```
nuget delete <packageID> <packageVersion> [options]
```

Burada `<packageID>` ve `<packageVersion>` unlist veya silmek için tam paketi belirleyin. Tam davranışı kaynağa bağlıdır. Yerel klasör için örneğin, paket silindi; nuget.org için listelenmeyen paketidir.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| apikey ile yapılan | Hedef depo API anahtarı. Mevcut bir belirtilen varsa *%AppData%\NuGet\NuGet.Config* kullanılır. |
| ConfigFile | *(2.5 +)*  Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır. |
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Kaynak | Sunucu URL'sini belirtir. Nuget.org URL'si `https://api.nuget.org/v3/index.json`. Örneğin, özel akışları için ana bilgisayar adı yerine *%hostname%/api/v3*. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *(2.5 +) ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
