---
title: NuGet CLI init komutu
description: Nuget.exe init komut başvurusu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4fda33aabd51fbbf0e5559baaa42af065366ba4
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817824"
---
# <a name="init-command-nuget-cli"></a>Init komutu (NuGet CLI)

**Uygulandığı öğe:** paketini oluşturma &bullet; **desteklenen sürümler:** 3.3 +

Tüm paketler için açıklandığı gibi hiyerarşik bir düzen kullanarak bir hedef klasöre düz bir klasörden kopyalar [Ekle komutu](cli-ref-add.md). Diğer bir deyişle, kullanarak `init` kullanmakla eşdeğerdir `add` klasöründeki her paketinizdeki komutu.

İle `add`, hedef bir yerel klasör veya bir UNC yolu; olmalıdır HTTP paket depoları nuget.org veya özel sunucuları gibi desteklenmez.

## <a name="usage"></a>Kullanım

```cli
nuget init <source> <destination> [options]
```

Burada `<source>` paketleri içeren klasör ve `<destination>` yerel klasör veya UNC pathname paketleri kopyalanır.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Genişletme | Paket kaynağı eklenen her paketindeki tüm dosyaları ekler; aynı `-Expand` ile `add` komutu. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| NonInteractive | Kullanıcı girişi veya onayı için ister gizler. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
