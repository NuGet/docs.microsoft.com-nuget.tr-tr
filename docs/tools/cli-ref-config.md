---
title: NuGet CLI config komutu
description: Nuget.exe config komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 376b69186ad22d4d94a1df51146b833a1f6f9bd9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546484"
---
# <a name="config-command-nuget-cli"></a>config komutu (NuGet CLI)

**İçin geçerlidir:** tüm &bullet; **desteklenen sürümler**: tüm

Alır veya NuGet yapılandırma değerlerini ayarlar. Ek kullanım için bkz: [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md). İzin verilen anahtar adları hakkında daha fazla bilgi için başvurmak [NuGet yapılandırma dosyası başvurusu](../reference/nuget-config-file.md).

## <a name="usage"></a>Kullanım

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

Burada `<name>` ve `<value>` yapılandırmada ayarlamak için bir anahtar-değer çifti belirtin. İstediğiniz gibi çok çiftleri belirtebilirsiniz. Bir değer kaldırmak için adını belirtin ve `=` oturum ancak herhangi bir değer.

İzin verilen anahtar adları için bkz [NuGet yapılandırma dosyası başvurusu](../reference/nuget-config-file.md).

NuGet 3.4 + içinde `<value>` kullanabilirsiniz [ortam değişkenlerini](cli-ref-environment-variables.md).

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| AsPath | Yapılandırma değeri bir yolu olarak döndürür yoksayıldı `-Set` kullanılır. |
| ConfigFile | Değiştirmek için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar. |
| Help | Bilgi komut için yardımı görüntüler. |
| NonInteractive | Kullanıcı girişini veya onaylar ister bastırır. |
| Verbosity | Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)

### <a name="examples"></a>Örnekler

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
