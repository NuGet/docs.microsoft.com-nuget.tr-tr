---
title: NuGet CLI init komutunu
description: Nuget.exe init komut başvurusu
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551416"
---
# <a name="init-command-nuget-cli"></a>init komutunu (NuGet CLI)

**İçin geçerlidir:** paket oluşturma &bullet; **desteklenen sürümler:** 3.3 +

Tüm paketler için açıklandığı gibi bir hiyerarşik yerleşim kullanarak bir hedef klasöre kopyalama yapan düz bir klasörden [Ekle komutu](cli-ref-add.md). Diğer bir deyişle, kullanarak `init` kullanmakla eşdeğerdir `add` klasöründeki her paket komutu.

Olduğu gibi `add`, hedef, yerel bir klasöre ya da bir UNC yolu; olmalıdır. Nuget.org veya özel sunucuları gibi HTTP paketinin depoları desteklenmez.

## <a name="usage"></a>Kullanım

```cli
nuget init <source> <destination> [options]
```

Burada `<source>` paketleri içeren klasör ve `<destination>` yerel klasör veya UNC pathname paketler kopyalanır.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar. |
| Genişletin | Paket kaynağı için eklenen her paketteki tüm dosyaları ekler; aynı `-Expand` ile `add` komutu. |
| Yardım | Bilgi komut için yardımı görüntüler. |
| NonInteractive | Kullanıcı girişini veya onaylar ister bastırır. |
| Ayrıntı Düzeyi | Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
