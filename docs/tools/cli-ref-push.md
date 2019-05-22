---
title: NuGet CLI anında iletme komutu
description: Nuget.exe anında iletme komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bce04864224a66019a52cdfff8355f68dc424204
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65974999"
---
# <a name="push-command-nuget-cli"></a>anında iletme komutu (NuGet CLI)

**İçin geçerlidir:** paket yayımlama &bullet; **desteklenen sürümler:** tüm; 4.1.0+ nuget.org için gerekli

> [!Important]
> Nuget.org için paketleri göndermeye nuget.exe verze 4.1.0 gerekli uygulayan + kullanmalısınız [NuGet protokolleri](../api/nuget-protocols.md).

Bir paket kaynağı için bir paket gönderir ve belgeyi yayımlar.

NuGet'ın varsayılan yapılandırmayı yükleyerek elde `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), ardından her yüklenirken `Nuget.Config` veya `.nuget\Nuget.Config` sürücüsünün kökünden başlayıp geçerli dizinde dosyaları (bkz [yapılandırma NuGet davranışını](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Kullanım

```cli
nuget push <packagePath> [options]
```

Burada `<packagePath>` sunucuya göndermek üzere paket tanımlar.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ApiKey | Hedef depo için API anahtarı. Yoksa, yapılandırma dosyasında belirtilen kullanılır. |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| DisableBuffering | Bellek kullanımları azaltmak için bir HTTP (s) sunucusuna gönderirken arabelleğe almayı devre dışı bırakır. Dikkat: Bu seçenek kullanıldığında, tümleşik Windows kimlik doğrulaması çalışmayabilir. |
| ForceEnglishOutput | *(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar. |
| Help | Bilgi komut için yardımı görüntüler. |
| NonInteractive | Kullanıcı girişini veya onaylar ister bastırır. |
| NoSymbols | *(3.5 +)*  Bir sembol paketi varsa, bunu bir simge sunucusuna gönderilecek değil. |
| Source | Sunucu URL'sini belirtir. NuGet, UNC veya yerel klasör kaynak tanımlar ve yalnızca HTTP kullanarak gönderme yerine dosya var. kopyalar.  Ayrıca, 3.4.2 NuGet ile başlayarak, zorunlu bir parametre sürece budur `NuGet.Config` dosyasını belirtir bir *DefaultPushSource* değeri (bkz [yapılandırma NuGet davranışını](../consume-packages/configuring-nuget-behavior.md)). |
| SkipDuplicate | Bir paket ve sürümü zaten atlayın ve sonraki paket anında varsa devam edin. |
| SymbolSource | *(3.5 +)*  Sembol sunucusunun URL'sini belirtir; nuget.smbsrc.net nuget.org için gönderirken kullanılan |
| SymbolApiKey | *(3.5 +)*  Belirtilen URL için API anahtarını belirtir `-SymbolSource`. |
| zaman aşımı | Bir sunucuya göndermek için saniye cinsinden zaman aşımı belirtir. 300 saniyedir (5 dakika) varsayılandır. |
| Verbosity | Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)

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
