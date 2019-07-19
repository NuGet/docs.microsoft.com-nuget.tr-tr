---
title: NuGet CLı Add komutu
description: NuGet. exe Add komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328362"
---
# <a name="add-command-nuget-cli"></a>Add komutu (NuGet CLı)

**Uygulama hedefi**: paket yayımlaması &bullet; **Desteklenen sürümler**: 3.3+

, Paket KIMLIĞI ve sürüm numarası için klasörler içinde oluşturulan, bir hiyerarşik düzende, belirtilen bir paketi HTTP olmayan bir kaynak (klasör veya UNC yolu) öğesine ekler. Örneğin:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

Paket kaynağına göre geri yükleme veya güncelleştirme yaparken hiyerarşik düzen önemli ölçüde daha iyi performans sağlar.

Paketteki tüm dosyaları hedef paket kaynağına genişletmek için `-Expand` anahtarını kullanın. Bu genellikle, `tools` ve `lib`gibi, hedefte görüntülenen ek alt klasörlere neden olur.

## <a name="usage"></a>Kullanım

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

, eklenecek paketin yol adı, ve `<sourcePath>` paketin ekleneceği klasör tabanlı paket kaynağını belirtir. `<packagePath>` HTTP kaynakları desteklenmez.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| Expand | Paketteki tüm dosyaları paket kaynağına ekler. |
| ForceEnglishOutput | *(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Help | Komut için yardım bilgilerini görüntüler. |
| NonInteractive | Kullanıcı girişi veya onayları için istemleri bastırır. |
| Verbosity | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
