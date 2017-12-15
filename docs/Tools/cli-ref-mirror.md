---
title: "NuGet CLI yansıtma komutu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 190d7010-172e-44b8-8a32-94a2a63be4f3
description: "Nuget.exe yansıtma komut başvurusu"
keywords: "nuget yansıtma başvuru, yansıtma komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67daa1aa278b42b7974c562ba4097a525e7bb105
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="mirror-command-nuget-cli"></a>Yansıtma komutu (NuGet CLI)

**Uygulandığı öğe:** paketini yayımlama &bullet; **desteklenen sürümler:** 3.2 +'da kullanım dışıdır

Bir paketi ve bağımlılıklarını belirtilen kaynak depoları öğesinden hedef depo yansıtır.

> [!NOTE]
> 3.2 önce NuGet sürümleri için bu komutu etkinleştirmek için şu adrese gidin [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), en yeni kararlı sürüm seçin, indirme `NuGet.ServerExtensions.dll` ve `Nuget-Signed.exe` yerel diske ve yeniden adlandırma `Nuget-Signed.exe` için `nuget.exe`.

## <a name="usage"></a>Kullanım

```
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

Burada `<packageID>` yansıtmak üzere paket veya `<configFilePath>` tanımlayan `packages.config` yansıtmak için paketlerini listeler dosya.

`<listUrlTarget>` Kaynak deposu belirtir ve `<publishUrlTarget>` hedef depo belirtir.

Hedef depo açıksa `https://machine/repo` çalıştıran [NuGet.Server](../hosting-packages/NuGet-Server.md), liste ve anında iletme URL'leri olacaktır `https://machine/repo/nuget` ve `https://machine/repo/api/v2/package`sırasıyla.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| apikey ile yapılan | Hedef depo API anahtarı. Mevcut bir belirtilen varsa *%AppData%\NuGet\NuGet.Config* kullanılır. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| NoCache | NuGet paketleri yerel makine önbellekleri kullanmalarını engeller. |
| Sekmeyi | Ne uygulanır ancak işlemleri gerçekleştirmez kaydeder; İtme işlemleri için başarı varsayar. |
| Yayın öncesi | Ön sürüm paketlerini yansıtma işlemi içerir. |
| Kaynak | Yansıtmak üzere paket kaynaklarının listesi. Dosyalardan herhangi bir kaynağa belirtilirse, tanımlanan *%AppData%\NuGet\NuGet.Config* , Hiçbiri belirtilmezse, nuget.org için varsayılan değer olarak kullanılır. |
| Zaman aşımı | Bir sunucuya gönderilmesi için saniye olarak zaman aşımını belirtir. 300 saniye (5 dakika) varsayılandır. |
| Sürüm | Yüklenecek paketin sürümü. Belirtilmezse, en son sürümünü yansıtılır. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
