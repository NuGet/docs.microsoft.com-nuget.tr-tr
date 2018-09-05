---
title: NuGet CLI komut ekleme
description: Nuget.exe için başvuru Ekle komutu
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545840"
---
# <a name="add-command-nuget-cli"></a>Ekle komutu (NuGet CLI)

**Uygulandığı**: Paket yayımlama &bullet; **desteklenen sürümler**: 3.3 +

Belirtilen paket için paket kimliği ve sürüm numarasını klasörler burada görüntülerle oluşturulur bir hiyerarşik düzende HTTP olmayan paket kaynağını (bir klasör veya UNC yolu) ekler. Örneğin:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Geri yükleme veya güncelleştirme karşı paket kaynağı, hiyerarşik yerleşim önemli ölçüde daha iyi performans sağlar.

Paketteki tüm dosyaların hedef paket kaynak genişletmek için kullanmak `-Expand` geçin. Bu genellikle hedef, aşağıdaki gibi görünen ek alt klasörlerinde sonuçları `tools` ve `lib`.

## <a name="usage"></a>Kullanım

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

Burada `<packagePath>` eklemek için paket için bir yol adı ve `<sourcePath>` , pakete eklenecek klasör tabanlı paket kaynağını belirtir. HTTP kaynakları desteklenmez.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| Genişletin | Tüm dosyalar paket kaynağına pakette ekler. |
| ForceEnglishOutput | *(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar. |
| Yardım | Bilgi komut için yardımı görüntüler. |
| NonInteractive | Kullanıcı girişini veya onaylar ister bastırır. |
| Ayrıntı Düzeyi | Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
