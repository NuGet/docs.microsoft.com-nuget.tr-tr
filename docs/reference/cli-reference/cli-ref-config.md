---
title: NuGet CLı yapılandırma komutu
description: NuGet. exe yapılandırma komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433314"
---
# <a name="config-command-nuget-cli"></a>config komutu (NuGet CLı)

**Uygulama hedefi:** &bullet; tüm **Desteklenen sürümler**: tümü

NuGet yapılandırma değerlerini alır veya ayarlar. Ek kullanım için bkz. [ortak NuGet yapılandırması](../../consume-packages/configuring-nuget-behavior.md). İzin verilen anahtar adları hakkında daha fazla bilgi için [NuGet yapılandırma dosyası başvurusuna](../nuget-config-file.md)bakın.

## <a name="usage"></a>Kullanım

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

Burada `<name>` ve`<value>` yapılandırmada ayarlanacak bir anahtar-değer çifti belirtin. İstediğiniz kadar çok çifti belirtebilirsiniz. Bir değeri kaldırmak için, adı ve `=` işareti belirtin ancak değeri belirtmeyin.

İzin verilen anahtar adları için bkz. [NuGet yapılandırma dosyası başvurusu](../nuget-config-file.md).

NuGet 3.4 + ' `<value>` da [ortam değişkenlerini](cli-ref-environment-variables.md)kullanabilir.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| AsPath | Yapılandırma değerini bir yol olarak döndürür, kullanıldığında yok sayılır `-Set` . |
| ConfigFile | Değiştirilecek NuGet yapılandırma dosyası. Belirtilmemişse, varsayılan dosya kullanılır-`%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.config/NuGet/NuGet.Config` (Mac/Linux) veya `~/.nuget/NuGet/NuGet.Config` (OS dağıtımına göre değişir).|
| ForceEnglishOutput | *(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Help | Komut için yardım bilgilerini görüntüler. |
| NonInteractive | Kullanıcı girişi veya onayları için istemleri bastırır. |
| Verbosity | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

### <a name="examples"></a>Örnekler

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
