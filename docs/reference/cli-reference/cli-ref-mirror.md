---
title: NuGet CLı yansıtma komutu
description: nuget.exe yansıtma komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a7247aeb21418e78dbfe9be15c2e7cd152aa3f4a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622973"
---
# <a name="mirror-command-nuget-cli"></a>Mirror komutu (NuGet CLı)

**Uygulama hedefi:** paket yayımlaması &bullet; **Desteklenen sürümler:** 3.2 + ' da kullanım dışı

Bir paketi ve onun bağımlılıklarını, belirtilen kaynak depolarından hedef depoya yansıtır.

> [!NOTE]
> Bu komutu daha önce NuGet 2. x içinde (NuGet-Signed.exe nuget.exe olarak yeniden adlandırarak) NuGet.ServerExtensions.dll ve NuGet-Signed.exe artık indirimıyordu. Şuna benzer bir komut kullanmak için [Nugetmirror](https://www.nuget.org/packages/NuGetMirror/)komutunu deneyin.

## <a name="usage"></a>Kullanım

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

, `<packageID>` yansıtmanın paketsidir veya `<configFilePath>` `packages.config` yansıtmak üzere paketleri listeleyen dosyayı tanımlar.

, `<listUrlTarget>` Kaynak depoyu belirtir ve `<publishUrlTarget>` Hedef depoyu belirtir.

Hedef deponuz `https://machine/repo` [NuGet. Server](../../hosting-packages/nuget-server.md)çalıştırıyorsa, liste ve gönderme URL 'leri `https://machine/repo/nuget` sırasıyla ve olur `https://machine/repo/api/v2/package` .

## <a name="options"></a>Seçenekler

- **`-ApiKey`**

  Hedef depo için API anahtarı. Mevcut değilse, yapılandırma dosyasında belirtilen bir tane kullanılır ( `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).

- **`-Help`**

  Komut için yardım bilgilerini görüntüler.

- **`-NoCache`**

  NuGet 'in önbelleğe alınmış paketleri kullanmasını engeller. Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-Noop`**

  Ne yapılacağını günlüğe kaydeder ancak eylemleri gerçekleştirmez; gönderme işlemleri için başarıyı varsayar.

- **`-PreRelease`**

  Yansıtma işlemindeki ön sürüm paketlerini içerir.

- **`-Source`**

  Yansıtmanın bir paket kaynakları listesi. Hiçbir kaynak belirtilmemişse, yapılandırma dosyasında (yukarıdaki ApiKey 'e bakın) tanımlanmış olanlar kullanılır, yoksa nuget.org varsayılan olarak belirlenir.

- **`-Timeout`**

  Bir sunucuya göndermek için saniye cinsinden zaman aşımını belirtir. Varsayılan değer 300 saniyedir (5 dakika).

- **`-Version`**

  Yüklenecek paketin sürümü. Belirtilmemişse, en son sürüm yansıtıldır.

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
