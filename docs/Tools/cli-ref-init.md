---
title: NuGet CLI init komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d413e4f3-1b41-4a92-8df8-87d21b542bd3
description: "Nuget.exe init komut başvurusu"
keywords: "nuget init başvuru, Init komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f63a3cbcca1aeff02995f23afd217c76e534b3be
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="init-command-nuget-cli"></a>Init komutu (NuGet CLI)

**Uygulandığı öğe:** paketini oluşturma &bullet; **desteklenen sürümler:** 3.3 +

Tüm paketler için açıklandığı gibi hiyerarşik bir düzen kullanarak bir hedef klasöre düz bir klasörden kopyalar [Ekle komutu](#add) üstünde. Diğer bir deyişle, kullanarak `init` kullanmakla eşdeğerdir `add` klasöründeki her paketinizdeki komutu.

İle `add`, hedef bir yerel klasör veya bir UNC yolu; olmalıdır HTTP paket depoları nuget.org veya özel sunucuları gibi desteklenmez.

## <a name="usage"></a>Kullanım

```
nuget init <source> <destination> [options]
```

Burada `<source>` paketleri içeren klasör ve `<destination>` yerel klasör veya UNC pathname olduğu paketleri kopyalanacak.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır. |
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Genişletme | Paket kaynağı eklenen her paketindeki tüm dosyaları ekler; aynı `-Expand` ile `add` komutu. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *(2.5 +) ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
