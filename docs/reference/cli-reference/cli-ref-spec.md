---
title: NuGet CLı spec komutu
description: NuGet. exe spec komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328275"
---
# <a name="spec-command-nuget-cli"></a>spec komutu (NuGet CLı)

**Uygulama hedefi:** paket oluşturma &bullet; **Desteklenen sürümler:** tümü

Yeni bir `.nuspec` paket için bir dosya oluşturur. Aynı klasörde bir proje dosyası (`.csproj`, `.vbproj`, `.fsproj`) ile çalıştırırsanız, `spec` simgeleştirilmiş `.nuspec` bir dosya oluşturur. Daha fazla bilgi için bkz. [paket oluşturma](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Kullanım

```cli
nuget spec [<packageID>] [options]
```

`<packageID>` , `.nuspec` dosyada kaydedilecek isteğe bağlı bir paket tanımlayıcısıdır.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| AssemblyPath | Meta veriler için kullanılacak derlemenin yolunu belirtir. |
| Zorla | Var olan `.nuspec` tüm dosyaların üzerine yazar. |
| ForceEnglishOutput | *(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Help | Komut için yardım bilgilerini görüntüler. |
| NonInteractive | Kullanıcı girişi veya onayları için istemleri bastırır. |
| Verbosity | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
