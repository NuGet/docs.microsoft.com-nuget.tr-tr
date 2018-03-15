---
title: NuGet CLI itme komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe itme komut başvurusu"
keywords: nuget push reference, push command
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 095e81406df3db5fbfc6c5202362894b2c6d7cf8
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/15/2018
---
# <a name="push-command-nuget-cli"></a>anında iletme komutu (NuGet CLI)

**Uygulandığı öğe:** paketini yayımlama &bullet; **desteklenen sürümler:** tüm; 4.1.0+ nuget.org için gerekli

> [!Important]
> Nuget.org için paketleri göndermek için nuget.exe v4.1.0 gerekli uygulayan + kullanmalısınız [NuGet protokolleri](../api/nuget-protocols.md).

Bir paket için paket kaynağı iter ve onu yayımlar.

NuGet'ın varsayılan yapılandırması yükleyerek elde edilir `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), ardından her yükleme `Nuget.Config` veya `.nuget\Nuget.Config` dosyaları sürücüsünün kökünden başlayıp geçerli dizinde (bkz [yapılandırma NuGet davranışı](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Kullanım

```cli
nuget push <packagePath> [options]
```

Burada `<packagePath>` sunucuya göndermek için paketi tanımlar.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ApiKey | Hedef depo API anahtarı. Yoksa, yapılandırma dosyasında belirtilen bir kullanılır. |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| DisableBuffering | Bellek kullanımları azaltmak için bir HTTP (s) sunucusuna iletme zaman arabelleğe almayı devre dışı bırakır. Uyarı: Bu seçenek kullanıldığında, tümleşik Windows kimlik doğrulaması çalışmayabilir. |
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| NoSymbols | *(3.5 +)*  Simge paketi varsa, onu bir simge sunucuya gönderilir değil. |
| Kaynak | Sunucu URL'sini belirtir. NuGet UNC veya yerel klasöre kaynak tanımlar ve yalnızca HTTP kullanarak gönderilmesi yerine dosya var. kopyalar.  Ayrıca, 3.4.2 NuGet ile başlayarak, bu zorunlu bir sürece parametredir `NuGet.Config` dosyayı belirtir bir *DefaultPushSource* değeri (bkz [NuGet yapılandırma davranışı](../consume-packages/configuring-nuget-behavior.md)). |
| SymbolSource | *(3.5 +)*  Simgesiyle sunucu URL belirtir; nuget.smbsrc.net için nuget.org Ftp'den zaman kullanılır |
| SymbolApiKey | *(3.5 +)*  URL belirtilen API anahtarını belirtir `-SymbolSource`. |
| Zaman aşımı | Bir sunucuya gönderilmesi için saniye olarak zaman aşımını belirtir. 300 saniye (5 dakika) varsayılandır. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

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

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
