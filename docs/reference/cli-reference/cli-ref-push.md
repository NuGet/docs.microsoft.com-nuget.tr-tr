---
title: NuGet CLı Push komutu
description: nuget.exe Push komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d53a2e7f41219e68e59b195d1d5a9d1f62ad7c63
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622853"
---
# <a name="push-command-nuget-cli"></a>Push komutu (NuGet CLı)

**Uygulama hedefi:** paket yayımlaması &bullet; **Desteklenen sürümler:** All; 4.1.0 + NuGet.org için gereklidir

> [!Important]
> Paketleri nuget.org 'e göndermek için gereken [NuGet protokollerini](../../api/nuget-protocols.md)uygulayan nuget.exe v 4.1.0 + kullanmanız gerekir.

Paketi bir paket kaynağına iter ve yayınlar.

NuGet 'in varsayılan yapılandırması `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) yüklenir, ardından `Nuget.Config` `.nuget\Nuget.Config` sürücü kökünden başlayıp geçerli dizinde (bkz. [ortak NuGet yapılandırmaları](../../consume-packages/configuring-nuget-behavior.md)) başlayarak veya dosya yüklendikten sonra alınır

## <a name="usage"></a>Kullanım

```cli
nuget push <packagePath> [options]
```

, `<packagePath>` sunucuya göndermek için paketi tanımlar.

## <a name="options"></a>Seçenekler

- **`-ApiKey`**

  Hedef depo için API anahtarı. Mevcut değilse, yapılandırma dosyasında belirtilen bir tane kullanılır.

- **`-ConfigFile`**

  Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.

- **`-DisableBuffering`**

  Bellek kullanımlarını azaltmak için bir HTTP (s) sunucusuna gönderilirken arabelleğe almayı devre dışı bırakır. Dikkat: Bu seçenek kullanıldığında, tümleşik Windows kimlik doğrulaması çalışmayabilir.

- **`-ForceEnglishOutput`**

  *(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.

- **`-?|-help`**

  Komut için yardım bilgilerini görüntüler.

- **`-NonInteractive`**

  Kullanıcı girişi veya onayları için istemleri bastırır.

- **`-NoServiceEndpoint`**

  `api/v2/packages`Kaynak URL 'ye eklemez.

- **`-NoSymbols`**

  *(3,5 +)* Bir semboller paketi varsa, bir sembol sunucusuna itilecektir.

- **`-src|-Source`**

  Sunucu URL 'sini belirtir. NuGet bir UNC veya yerel klasör kaynağını tanımlar ve dosyayı HTTP kullanarak göndermek yerine buraya kopyalar.  Ayrıca, NuGet 3.4.2 ile başlayarak, `NuGet.Config` dosya bir *Defaultpushsource* değeri belirtmediği müddetçe bu zorunlu bir parametredir (bkz. [NuGet davranışını yapılandırma](../../consume-packages/configuring-nuget-behavior.md)).

- **`-SkipDuplicate`**

  *(5.1 +)* Bir paket ve sürüm zaten varsa, bunu atlayın ve varsa gönderim içindeki bir sonraki pakete devam edin.

- **`-SymbolSource`**

  *(3,5 +)* Sembol sunucusu URL 'sini belirtir; nuget.org 'e gönderilirken nuget.smbsrc.net kullanılır

- **`-SymbolApiKey`**

  *(3,5 +)* İçinde belirtilen URL için API anahtarını belirtir `-SymbolSource` .

- **`-Timeout`**

  Bir sunucuya göndermek için saniye cinsinden zaman aşımını belirtir. Varsayılan değer 300 saniyedir (5 dakika).

- **`-Verbosity [normal|quiet|detailed]`**

  Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .


Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
