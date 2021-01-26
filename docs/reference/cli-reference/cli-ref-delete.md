---
title: NuGet CLı Delete komutu
description: nuget.exe Delete komutu için başvuru
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 96c75366ae69b34f5cd1f55feb53087b5d0ea324
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775947"
---
# <a name="delete-command-nuget-cli"></a>Delete komutu (NuGet CLı)

**Uygulama hedefi:** paket yayımlaması &bullet; **Desteklenen sürümler:** tümü

Paket kaynağından bir paketi siler veya listesini kaldırır. Nuget.org için, Delete komutu [paketin listesini kaldırır](../../nuget-org/policies/deleting-packages.md).

## <a name="usage"></a>Kullanım

```cli
nuget delete <packageID> <packageVersion> [options]
```

`<packageID>` `<packageVersion>` silmek veya listeden kaldırmak için tam paketi burada ve belirler. Tam davranış kaynağa bağlıdır. Örneğin, yerel klasörler için, paket silinir; nuget.org için paket listelenmemiş değildir.

## <a name="options"></a>Seçenekler

- **`-ApiKey`**

  Hedef depo için API anahtarı. Mevcut değilse, yapılandırma dosyasında belirtilen bir tane kullanılır.

- **`-ConfigFile`**

  Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.

- **`-ForceEnglishOutput`**

  *(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.

- **`-?|-help`**

  Komut için yardım bilgilerini görüntüler.

- **`-NonInteractive`**

  Kullanıcı girişi veya onayları için istemleri bastırır.

 - **`-np|-NoPrompt`**

   Silme sırasında sorma.

 - **`-NoServiceEndpoint`** Kaynak URL 'ye "API/v2/paket" eklemez.

- **`-src|-Source`**

  Sunucu URL 'sini belirtir. Nuget.org URL 'SI `https://api.nuget.org/v3/index.json` . Özel akışlar için ana bilgisayar adını (örneğin, *% hostname%/api/v3*) değiştirin.

- **`-Verbosity [normal|quiet|detailed]`**

  Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
