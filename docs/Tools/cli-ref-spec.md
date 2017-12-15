---
title: NuGet CLI belirtim komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Nuget.exe belirtim komut başvurusu"
keywords: "nuget belirtim başvurusu, belirtim komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a>belirtim komutu (NuGet CLI)

**Uygulandığı öğe:** paketini oluşturma &bullet; **desteklenen sürümler:** tüm

Oluşturan bir `.nuspec` dosyası yeni bir paket için. Proje dosyası ile aynı klasörde çalıştırırsanız (`.csproj`, `.vbproj`, `.fsproj`), `spec` bir parçalanmış oluşturur `.nuspec` dosya. Ek bilgi için bkz: [paket oluşturma](../create-packages/creating-a-package.md).

## <a name="usage"></a>Kullanım

```
nuget spec [<packageID>] [options]
```

Burada `<packageID>` kaydetmek için bir isteğe bağlı paket tanımlayıcısı `.nuspec` dosya.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| AssemblyPath | Meta veriler için kullanmak için derleme yolunu belirtir. |
| Zorla | Var olan üzerine yazar `.nuspec` dosya. |
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *(2.5 +) ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
