---
title: NuGet CLI yansıtma komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe yansıtma komut başvurusu
keywords: nuget yansıtma başvuru, yansıtma komutu
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 512bd72d568cda81eb7c6a1555c36ead66b5c438
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="mirror-command-nuget-cli"></a>Yansıtma komutu (NuGet CLI)

**Uygulandığı öğe:** paketini yayımlama &bullet; **desteklenen sürümler:** 3.2 +'da kullanım dışıdır

Bir paketi ve bağımlılıklarını belirtilen kaynak depoları öğesinden hedef depo yansıtır.

> [!NOTE]
> 3.2 önce NuGet sürümleri için bu komutu etkinleştirmek için şu adrese gidin [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), en yeni kararlı sürüm seçin, indirme `NuGet.ServerExtensions.dll` ve `Nuget-Signed.exe` yerel diske ve yeniden adlandırma `Nuget-Signed.exe` için `nuget.exe`.

## <a name="usage"></a>Kullanım

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

Burada `<packageID>` yansıtmak üzere paket veya `<configFilePath>` tanımlayan `packages.config` yansıtmak için paketlerini listeler dosya.

`<listUrlTarget>` Kaynak deposu belirtir ve `<publishUrlTarget>` hedef depo belirtir.

Hedef depo açıksa `https://machine/repo` çalıştıran [NuGet.Server](../hosting-packages/nuget-server.md), liste ve anında iletme URL'leri olacaktır `https://machine/repo/nuget` ve `https://machine/repo/api/v2/package`sırasıyla.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ApiKey | Hedef depo API anahtarı. Yoksa, yapılandırma dosyasında belirtilen bir kullanılıp kullanılmadığını (`%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| NoCache | NuGet kullanarak önbelleğe alınmış paketleri engeller. Bkz: [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| Sekmeyi | Ne uygulanır ancak işlemleri gerçekleştirmez kaydeder; İtme işlemleri için başarı varsayar. |
| Yayın öncesi | Ön sürüm paketlerini yansıtma işlemi içerir. |
| Kaynak | Yansıtmak üzere paket kaynaklarının listesi. Dosyalardan herhangi bir kaynağa belirtilirse, tanımlanan yapılandırma dosyası (apikey ile yapılan yukarıdaki bakın) kullanılır, nuget.org için Hiçbiri belirtilmezse, varsayılan olarak ayarlanıyor. |
| Zaman aşımı | Bir sunucuya gönderilmesi için saniye olarak zaman aşımını belirtir. 300 saniye (5 dakika) varsayılandır. |
| Sürüm | Yüklenecek paketin sürümü. Belirtilmezse, en son sürümünü yansıtılır. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
