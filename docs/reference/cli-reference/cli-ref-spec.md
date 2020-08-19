---
title: NuGet CLı spec komutu
description: nuget.exe spec komutu başvurusu
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622570"
---
# <a name="spec-command-nuget-cli"></a>spec komutu (NuGet CLı)

**Uygulama hedefi:** paket oluşturma &bullet; **Desteklenen sürümler:** tümü

`.nuspec`Yeni bir paket için bir dosya oluşturur. Aynı klasörde bir proje dosyası ( `.csproj` , `.vbproj` ,) ile çalıştırırsanız `.fsproj` , `spec` simgeleştirilmiş bir `.nuspec` dosya oluşturur. Daha fazla bilgi için bkz. [paket oluşturma](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Kullanım

```cli
nuget spec [<packageID>] [options]
```

, `<packageID>` dosyada kaydedilecek isteğe bağlı bir paket tanımlayıcısıdır `.nuspec` .

## <a name="options"></a>Seçenekler

- **`-AssemblyPath`**

  Meta veriler için kullanılacak derlemenin yolunu belirtir.

- **`-Force`**

  Var olan tüm `.nuspec` dosyaların üzerine yazar.


- **`-ForceEnglishOutput`**

  *(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.

- **`-?|-help`**

  Komut için yardım bilgilerini görüntüler.

- **`-NonInteractive`**

  Kullanıcı girişi veya onayları için istemleri bastırır.

- **`-Verbosity [normal|quiet|detailed]`**

  Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
