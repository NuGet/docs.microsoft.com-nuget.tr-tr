---
title: NuGet CLı init komutu
description: NuGet. exe init komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328338"
---
# <a name="init-command-nuget-cli"></a>init komutu (NuGet CLı)

**Uygulama hedefi:** paket oluşturma &bullet; **Desteklenen sürümler:** 3.3+

Bir düz klasörden tüm paketleri, [Add komutunda](cli-ref-add.md)açıklandığı gibi hiyerarşik bir düzen kullanarak bir hedef klasöre kopyalar. Diğer bir deyişle, `init` bu, klasöründeki her pakette `add` komutunu kullanmakla eşdeğerdir.

İle `add`olduğu gibi, hedef yerel bir klasör ya da bir UNC yolu olmalıdır; Nuget.org veya özel sunucular gibi HTTP paket depoları desteklenmez.

## <a name="usage"></a>Kullanım

```cli
nuget init <source> <destination> [options]
```

, paketleri içeren klasördür ve `<destination>` paketlerin kopyalandığı yerel klasör veya UNC yol adı olur. `<source>`

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Expand | Paket kaynağına eklenen her pakette bulunan tüm dosyaları ekler; `-Expand` komutuyla aynı`add` . |
| Help | Komut için yardım bilgilerini görüntüler. |
| NonInteractive | Kullanıcı girişi veya onayları için istemleri bastırır. |
| Verbosity | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
