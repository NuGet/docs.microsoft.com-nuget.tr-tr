---
title: NuGet CLI config komutu
description: Nuget.exe yapılandırma komut başvurusu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 9deab9fcca740ea99da61b7d54700a29c1813e88
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818171"
---
# <a name="config-command-nuget-cli"></a>config komutunu (NuGet CLI)

**Uygulandığı öğe:** tüm &bullet; **desteklenen sürümleri**: tüm

Alır veya NuGet yapılandırma değerlerini ayarlar. Ek kullanım için bkz: [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md). İzin verilen anahtar adları hakkında daha fazla bilgi için başvurmak [NuGet yapılandırma dosyası başvurusu](../reference/nuget-config-file.md).

## <a name="usage"></a>Kullanım

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

Burada `<name>` ve `<value>` yapılandırmada ayarlamak için bir anahtar-değer çifti belirtin. Sayıda çiftleri istendiği gibi belirtebilirsiniz. Bir değer kaldırmak için ad belirtin ve `=` oturum ancak hiçbir değer.

İzin verilen anahtar adları için bkz: [NuGet yapılandırma dosyası başvurusu](../reference/nuget-config-file.md).

NuGet 3.4 + içinde `<value>` kullanabilirsiniz [ortam değişkenleri](cli-ref-environment-variables.md).

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| AsPath | Yapılandırma değeri bir yolu olarak döndürür yoksayıldı `-Set` kullanılır. |
| ConfigFile | Değiştirmek için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| NonInteractive | Kullanıcı girişi veya onayı için ister gizler. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

### <a name="examples"></a>Örnekler

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
