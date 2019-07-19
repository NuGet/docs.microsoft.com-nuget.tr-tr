---
title: NuGet CLı Push komutu
description: NuGet. exe Push komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328293"
---
# <a name="push-command-nuget-cli"></a>Push komutu (NuGet CLı)

**Uygulama hedefi:** paket yayımlaması &bullet; **Desteklenen sürümler:** All; 4.1.0 + NuGet.org için gereklidir

> [!Important]
> Paketleri nuget.org 'e göndermek için gereken [NuGet protokollerini](../../api/nuget-protocols.md)uygulayan NuGet. exe v 4.1.0 + kullanmanız gerekir.

Paketi bir paket kaynağına iter ve yayınlar.

NuGet 'in varsayılan yapılandırması `%AppData%\NuGet\NuGet.Config` , (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) yüklenir, ardından sürücü kökünden başlayıp geçerli dizinde `.nuget\Nuget.Config` sona ermek üzere herhangi bir `Nuget.Config` veya dosya yükleniyor (bkz. [ortak NuGet yapılandırma](../../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Kullanım

```cli
nuget push <packagePath> [options]
```

, sunucuya göndermek için paketi tanımlar.`<packagePath>`

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ApiKey | Hedef depo için API anahtarı. Mevcut değilse, yapılandırma dosyasında belirtilen bir tane kullanılır. |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| Disablearabelleğe alma | Bellek kullanımlarını azaltmak için bir HTTP (s) sunucusuna gönderilirken arabelleğe almayı devre dışı bırakır. Dikkat: Bu seçenek kullanıldığında, tümleşik Windows kimlik doğrulaması çalışmayabilir. |
| ForceEnglishOutput | *(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Help | Komut için yardım bilgilerini görüntüler. |
| NonInteractive | Kullanıcı girişi veya onayları için istemleri bastırır. |
| NoSymbols | *(3,5 +)* Bir semboller paketi varsa, bir sembol sunucusuna itilecektir. |
| Source | Sunucu URL 'sini belirtir. NuGet bir UNC veya yerel klasör kaynağını tanımlar ve dosyayı HTTP kullanarak göndermek yerine buraya kopyalar.  Ayrıca, NuGet 3.4.2 ile başlayarak, `NuGet.Config` dosya bir *defaultpushsource* değeri belirtmediği müddetçe bu zorunlu bir parametredir (bkz. [NuGet davranışını yapılandırma](../../consume-packages/configuring-nuget-behavior.md)). |
| SkipDuplicate | *(5.1 +)* Bir paket ve sürüm zaten varsa, bunu atlayın ve varsa gönderim içindeki bir sonraki pakete devam edin. |
| SymbolSource | *(3,5 +)* Sembol sunucusu URL 'sini belirtir; nuget.org 'e gönderilirken nuget.smbsrc.net kullanılır |
| Sembolapikey | *(3,5 +)* İçinde `-SymbolSource`BELIRTILEN URL için API anahtarını belirtir. |
| zaman aşımı | Bir sunucuya göndermek için saniye cinsinden zaman aşımını belirtir. Varsayılan değer 300 saniyedir (5 dakika). |
| Verbosity | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

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
