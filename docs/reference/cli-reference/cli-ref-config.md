---
title: NuGet CLı yapılandırma komutu
description: nuget.exe config komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7d0c1c51f40cba9a5b69f209ffbd995451bfeb9f
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622882"
---
# <a name="config-command-nuget-cli"></a>config komutu (NuGet CLı)

**Uygulama hedefi:** tüm &bullet; **Desteklenen sürümler**: tümü

NuGet yapılandırma değerlerini alır veya ayarlar. Ek kullanım için bkz. [ortak NuGet yapılandırması](../../consume-packages/configuring-nuget-behavior.md). İzin verilen anahtar adları hakkında daha fazla bilgi için [NuGet yapılandırma dosyası başvurusuna](../nuget-config-file.md)bakın.

## <a name="usage"></a>Kullanım

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

Burada `<name>` ve `<value>` yapılandırmada ayarlanacak bir anahtar-değer çifti belirtin. İstediğiniz kadar çok çifti belirtebilirsiniz. Bir değeri kaldırmak için, adı ve `=` işareti belirtin ancak değeri belirtmeyin.

İzin verilen anahtar adları için bkz. [NuGet yapılandırma dosyası başvurusu](../nuget-config-file.md).

NuGet 3.4 + ' da `<value>` [ortam değişkenlerini](cli-ref-environment-variables.md)kullanabilir.

## <a name="options"></a>Seçenekler


- **`AsPath`**

  Yapılandırma değerini bir yol olarak döndürür, kullanıldığında yok sayılır `-Set` .

- **`-ConfigFile`**

  Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.

- **`-ForceEnglishOutput`**

  *(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.

- **`-?|-help`**

  Komut için yardım bilgilerini görüntüler.

- **`-NonInteractive`**

  Kullanıcı girişi veya onayları için istemleri bastırır.

- **`-Set`**

  Yapılandırma içinde ayarlanacak daha fazla anahtar-değer çiftinden biridir.

- **`-Verbosity [normal|quiet|detailed]`**

  Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

### <a name="examples"></a>Örnekler

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
