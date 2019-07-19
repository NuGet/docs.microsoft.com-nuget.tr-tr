---
title: NuGet CLı kaynakları komutu
description: NuGet. exe kaynakları komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328284"
---
# <a name="sources-command-nuget-cli"></a>Sources komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi, yayımlama &bullet; **Desteklenen sürümler:** tümü

Kullanıcı kapsamı yapılandırma dosyasında veya belirtilen yapılandırma dosyasında bulunan kaynak listesini yönetir. Kullanıcı kapsamı yapılandırma dosyası (Windows) ve `%appdata%\NuGet\NuGet.Config` `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) konumunda bulunur.

Nuget.org için kaynak URL 'sinin olduğunu `https://api.nuget.org/v3/index.json`unutmayın.

## <a name="usage"></a>Kullanım

```cli
nuget sources <operation> -Name <name> -Source <source>
```

Burada `<operation>` bir *liste, ekleme, kaldırma, etkinleştirme, devre dışı bırakma* veya *güncelleştirme* `<name>` , kaynağın adı ve `<source>` kaynağın URL 'si olduğu yerdir. Tek seferde yalnızca bir kaynak üzerinde işlem yapabilirsiniz.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Biçimi | Eyleme uygulanır ve `Detailed` (varsayılan) veya `Short`olabilir. `list` |
| Help | Komut için yardım bilgilerini görüntüler. |
| NonInteractive | Kullanıcı girişi veya onayları için istemleri bastırır. |
| Parola | Kaynakla kimlik doğrulaması için parolayı belirtir. |
| Storepasswordincöğrentext | Şifrelenmiş bir form depolamanın varsayılan davranışı yerine parolayı şifrelenmemiş metin olarak depolamayı gösterir. |
| UserName | Kaynakla kimlik doğrulaması için Kullanıcı adını belirtir. |
| Verbosity | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

> [!Note]
> Paket kaynağına erişmek için NuGet. exe ' nin daha sonra kullanıldığından, kaynakların parolasını aynı kullanıcı bağlamında eklediğinizden emin olun. Parola yapılandırma dosyasında şifrelenmiş olarak depolanır ve yalnızca, şifrelendiğinden aynı kullanıcı bağlamında şifresi çözülür. Örneğin, NuGet paketlerini geri yüklemek için bir yapı sunucusu kullandığınızda, parola, yapı sunucusu görevinin çalışacağı aynı Windows kullanıcıyla şifrelenmelidir.

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
