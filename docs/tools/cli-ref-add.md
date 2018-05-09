---
title: NuGet CLI Ekle komutu
description: Nuget.exe için başvuru Ekle komutu
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4a4201a321ffe0f7fb61f4e98012a1a2d7d8fda4
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="add-command-nuget-cli"></a>Ekle komutu (NuGet CLI)

**Uygulandığı öğe**: paketini yayımlama &bullet; **desteklenen sürümleri**: 3.3 +

Belirli bir paket (bir klasör veya UNC yolu) HTTP olmayan paket kaynağı klasörler için paket kimliği ve sürüm numarası; burada görüntülerle oluşturulan bir hiyerarşik düzende ekler. Örneğin:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Geri yükleme veya paket kaynağında Güncelleştirme sırasında hiyerarşik düzeni önemli ölçüde daha iyi performans sağlar.

Paketteki tüm dosyaları hedef paket kaynağına genişletmek için kullanmak `-Expand` geçin. Bu genellikle hedef gibi görünen ek alt klasörler sonuçları `tools` ve `lib`.

## <a name="usage"></a>Kullanım

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

Burada `<packagePath>` eklemek için paket için yol adı ve `<sourcePath>` için paket eklenecek klasör tabanlı paket kaynağını belirtir. HTTP kaynakları desteklenmez.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| Genişletme | Tüm dosyalar paket kaynağına pakette ekler. |
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
