---
title: NuGet CLI Ekle komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 4f68a016-ad4e-41fc-b869-88910fc5121e
description: "Nuget.exe için başvuru Ekle komutu"
keywords: "nuget başvuru eklemek için paket komut ekleme"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bf9a6e51dfbf1716ba40273487b76ae04c18e948
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
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

```
nuget add <packagePath> -Source <sourcePath> [options]
```

Burada `<packagePath>` eklemek için paket için yol adı ve `<sourcePath>` için paket eklenecek klasör tabanlı paket kaynağını belirtir. HTTP kaynakları desteklenmez.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.| 
| Genişletme | Tüm dosyalar paket kaynağına pakette ekler. |
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
