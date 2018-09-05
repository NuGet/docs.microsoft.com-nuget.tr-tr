---
title: NuGet CLI yansıtma komutu
description: Nuget.exe yansıtma komut başvurusu
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550212"
---
# <a name="mirror-command-nuget-cli"></a>Yansıtma komutu (NuGet CLI)

**İçin geçerlidir:** paket yayımlama &bullet; **desteklenen sürümler:** 3.2 +'da kullanım dışı

Bir paketi ve bağımlılıkları belirtilen kaynak depolardan hedef depoda yansıtır.

> [!NOTE]
> Bu komut için NuGet sürümü 3.2 önce etkinleştirmek için Git [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), en yeni kararlı bir sürüm seçmek, indirme `NuGet.ServerExtensions.dll` ve `Nuget-Signed.exe` yerel diskinize ve yeniden adlandırma `Nuget-Signed.exe` için `nuget.exe`.

## <a name="usage"></a>Kullanım

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

Burada `<packageID>` yansıtmak için paket veya `<configFilePath>` tanımlayan `packages.config` yansıtmak için paketlerini listeler dosya.

`<listUrlTarget>` Kaynak deposu belirtir ve `<publishUrlTarget>` hedef depoyu belirtir.

Hedef depoyu açıksa `https://machine/repo` çalıştıran [NuGet.Server](../hosting-packages/nuget-server.md), liste ve anında iletme URL'leri olacaktır `https://machine/repo/nuget` ve `https://machine/repo/api/v2/package`sırasıyla.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ApiKey | Hedef depo için API anahtarı. Mevcut yapılandırma dosyasında belirtilen kullanılıp kullanılmadığını (`%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| Yardım | Bilgi komut için yardımı görüntüler. |
| NoCache | NuGet, önbelleğe eklenen paketler kullanmasını önler. Bkz: [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| Noop | Ne olduğu, ancak işlemleri gerçekleştirmez günlüğe kaydeder; Gönderme işlemleri için başarı varsayar. |
| Yayın öncesi | Yayın öncesi paketleri yansıtma işlemi içerir. |
| Kaynak | Yansıtmak için paket kaynaklarının listesi. Olanlara kaynak belirtilirse, tanımlanan yapılandırma dosyası (bkz. Yukarıdaki ApiKey) kullanılır, nuget.org için hiçbir şey belirtilmezse varsayılan olarak ayarlanıyor. |
| zaman aşımı | Bir sunucuya göndermek için saniye cinsinden zaman aşımı belirtir. 300 saniyedir (5 dakika) varsayılandır. |
| Sürüm | Yüklemek için Paket sürümü. Belirtilmezse, en son sürüme yansıtılır. |

Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
