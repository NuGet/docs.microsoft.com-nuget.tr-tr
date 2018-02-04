---
title: NuGet CLI belirtim komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe belirtim komut başvurusu"
keywords: "nuget belirtim başvurusu, belirtim komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc7e772e737a0f74929d13e2b126f7796b6d0dc7
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="spec-command-nuget-cli"></a>belirtim komutu (NuGet CLI)

**Uygulandığı öğe:** paketini oluşturma &bullet; **desteklenen sürümler:** tüm

Oluşturan bir `.nuspec` dosyası yeni bir paket için. Proje dosyası ile aynı klasörde çalıştırırsanız (`.csproj`, `.vbproj`, `.fsproj`), `spec` bir parçalanmış oluşturur `.nuspec` dosya. Ek bilgi için bkz: [paket oluşturma](../create-packages/creating-a-package.md).

## <a name="usage"></a>Kullanım

```cli
nuget spec [<packageID>] [options]
```

Burada `<packageID>` kaydetmek için bir isteğe bağlı paket tanımlayıcısı `.nuspec` dosya.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| AssemblyPath | Meta veriler için kullanmak için derleme yolunu belirtir. |
| Force | Var olan üzerine yazar `.nuspec` dosya. |
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
