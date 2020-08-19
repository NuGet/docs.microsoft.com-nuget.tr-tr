---
title: NuGet CLı kaynakları komutu
description: nuget.exe Sources komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 73c9cea8200a1ab1937d25a9a611ae7f2a943dba
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622596"
---
# <a name="sources-command-nuget-cli"></a>Sources komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi, yayımlama &bullet; **Desteklenen sürümler:** tümü

Kullanıcı kapsamı yapılandırma dosyasında veya belirtilen yapılandırma dosyasında bulunan kaynak listesini yönetir. Kullanıcı kapsamı yapılandırma dosyası `%appdata%\NuGet\NuGet.Config` (Windows) ve `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) konumunda bulunur.

Nuget.org için kaynak URL 'sinin olduğunu unutmayın `https://api.nuget.org/v3/index.json` .

## <a name="usage"></a>Kullanım

```cli
nuget sources <operation> -Name <name> -Source <source>
```

Burada `<operation>` bir *liste, ekleme, kaldırma, etkinleştirme, devre dışı bırakma* veya *güncelleştirme*, `<name>` kaynağın adı ve `<source>` kaynağın URL 'si olduğu yerdir. Tek seferde yalnızca bir kaynak üzerinde işlem yapabilirsiniz.

## <a name="options"></a>Seçenekler

- **`-ConfigFile`**

  Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.

- **`-ForceEnglishOutput`**

  *(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.

- **`-Format`**

  `list`Eyleme uygulanır ve `Detailed` (varsayılan) veya olabilir `Short` .

- **`-?|-help`**

  Komut için yardım bilgilerini görüntüler.

- **`-Name`**

  Kaynağın adı.

- **`-NonInteractive`**

  Kullanıcı girişi veya onayları için istemleri bastırır.

- **`-Password`**

  Kaynakla kimlik doğrulaması için parolayı belirtir.

- **`-src|-Source`**

  Paket (ler) kaynağının yolu.

- **`-StorePasswordInClearText`**

  Şifrelenmiş bir form depolamanın varsayılan davranışı yerine parolayı şifrelenmemiş metin olarak depolamayı gösterir.

- **`-UserName`**

  Kaynakla kimlik doğrulaması için Kullanıcı adını belirtir.

- **`-ValidAuthenticationTypes`**

  Bu kaynak için geçerli kimlik doğrulama türlerinin virgülle ayrılmış listesi. Varsayılan olarak, tüm kimlik doğrulama türleri geçerlidir. Örnek: `basic,negotiate`.

- **`-Verbosity [normal|quiet|detailed]`**

  Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .

> [!Note]
> Daha sonra paket kaynağına erişmek için nuget.exe, kaynakların parolasını aynı kullanıcı bağlamına eklediğinizden emin olun. Parola yapılandırma dosyasında şifrelenmiş olarak depolanır ve yalnızca, şifrelendiğinden aynı kullanıcı bağlamında şifresi çözülür. Örneğin, NuGet paketlerini geri yüklemek için bir yapı sunucusu kullandığınızda, parola, yapı sunucusu görevinin çalışacağı aynı Windows kullanıcıyla şifrelenmelidir.

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
