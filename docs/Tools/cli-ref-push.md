---
title: NuGet CLI itme komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a9709eee-add2-47fb-98e6-eec0697087f6
description: "Nuget.exe itme komut başvurusu"
keywords: "nuget itme başvuru, anında iletme komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2828cdc41903d8a948870155b23721724bfa781e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="push-command-nuget-cli"></a>anında iletme komutu (NuGet CLI)

**Uygulandığı öğe:** paketini yayımlama &bullet; **desteklenen sürümler:** tüm; 4.1.0+ nuget.org için gerekli

> [!Important]
> Nuget.org için paketleri göndermek için nuget.exe v4.1.0 gerekli uygulayan + kullanmalısınız [NuGet protokolleri](../api/nuget-protocols.md).

Bir paket için paket kaynağı iter ve onu yayımlar.

NuGet'ın varsayılan yapılandırması yükleyerek elde edilir `%AppData%\NuGet\NuGet.Config`, herhangi bir yükleme sonra `Nuget.Config` veya `.nuget\Nuget.Config` dosyaları sürücüsünün kökünden başlayıp geçerli dizinde (bkz [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>Kullanım

```
nuget push <packagePath> [options]
```

Burada `<packagePath>` sunucuya göndermek için paketi tanımlar.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| apikey ile yapılan | Hedef depo API anahtarı. Mevcut bir belirtilen varsa *%AppData%\NuGet\NuGet.Config* kullanılır. |
| ConfigFile | *(2.5 +)*  Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır. |
| DisableBuffering | Bellek kullanımları azaltmak için bir HTTP (s) sunucusuna iletme zaman arabelleğe almayı devre dışı bırakır. Uyarı: Bu seçenek kullanıldığında, tümleşik Windows kimlik doğrulaması çalışmayabilir. |
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| NoSymbols | *(3.5 +)*  Simge paketi varsa, onu bir simge sunucuya gönderilir değil. |
| Kaynak | Sunucu URL'sini belirtir. NuGet ile 2.5 +, NuGet UNC veya yerel klasöre kaynak belirleyin ve yalnızca HTTP kullanarak gönderilmesi yerine dosyayı var. kopyalayın.  Ayrıca, 3.4.2 NuGet ile başlayarak, bu zorunlu bir sürece parametredir `NuGet.Config` dosyayı belirtir bir *DefaultPushSource* değeri (bkz [NuGet yapılandırma davranışı](../Consume-Packages/Configuring-NuGet-Behavior.md)). |
| SymbolSource | *(3.5 +)*  Simgesiyle sunucu URL belirtir; nuget.smbsrc.net için nuget.org Ftp'den zaman kullanılır |
| SymbolApiKey | *(3.5 +)*  URL belirtilen API anahtarını belirtir `-SymbolSource`. |
| Zaman aşımı | Bir sunucuya gönderilmesi için saniye olarak zaman aşımını belirtir. 300 saniye (5 dakika) varsayılandır. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *(2.5 +) ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
