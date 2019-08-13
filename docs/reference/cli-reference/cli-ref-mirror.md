---
title: NuGet CLı yansıtma komutu
description: NuGet. exe yansıtma komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 81866172bfbf55c42ee96c213c0117f1f986235c
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959719"
---
# <a name="mirror-command-nuget-cli"></a>Mirror komutu (NuGet CLı)

**Uygulama hedefi:** paket yayımlaması &bullet; **Desteklenen sürümler:** 3.2 + ' da kullanım dışı

Bir paketi ve onun bağımlılıklarını, belirtilen kaynak depolarından hedef depoya yansıtır.

> [!NOTE]
> NuGet 2. x (NuGet-Signed. exe ' yi NuGet. exe ' ye yeniden adlandırarak) bu komutu daha önce destekleyen NuGet. ServerExtensions. dll ve NuGet-Signed. exe artık indirimıyordu. Şuna benzer bir komut kullanmak için [Nugetmirror](https://www.nuget.org/packages/NuGetMirror/)komutunu deneyin.

## <a name="usage"></a>Kullanım

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

, yansıtmanın paketsidir veya `<configFilePath>` yansıtmak üzere paketleri listeleyen `packages.config` dosyayı tanımlar. `<packageID>`

, `<listUrlTarget>` Kaynak depoyu belirtir ve `<publishUrlTarget>` hedef depoyu belirtir.

Hedef deponuz `https://machine/repo` [NuGet. Server](../../hosting-packages/nuget-server.md)çalıştırıyorsa, liste ve `https://machine/repo/nuget` gönderme URL 'leri sırasıyla ve `https://machine/repo/api/v2/package`olur.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ApiKey | Hedef depo için API anahtarı. Mevcut değilse, yapılandırma dosyasında belirtilen bir tane kullanılır (`%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)). |
| Help | Komut için yardım bilgilerini görüntüler. |
| NoCache | NuGet 'in önbelleğe alınmış paketleri kullanmasını engeller. Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NOOP | Ne yapılacağını günlüğe kaydeder ancak eylemleri gerçekleştirmez; gönderme işlemleri için başarıyı varsayar. |
| Sp1'in | Yansıtma işlemindeki ön sürüm paketlerini içerir. |
| Source | Yansıtmanın bir paket kaynakları listesi. Hiçbir kaynak belirtilmemişse, yapılandırma dosyasında (yukarıdaki ApiKey 'e bakın) tanımlanmış olanlar kullanılır, yoksa nuget.org varsayılan olarak belirlenir. |
| zaman aşımı | Bir sunucuya göndermek için saniye cinsinden zaman aşımını belirtir. Varsayılan değer 300 saniyedir (5 dakika). |
| Sürüm | Yüklenecek paketin sürümü. Belirtilmemişse, en son sürüm yansıtıldır. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
