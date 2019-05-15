---
title: NuGet CLI komutu kaynakları
description: Komut nuget.exe için başvuru kaynakları
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610629"
---
# <a name="sources-command-nuget-cli"></a>kaynakları komut (NuGet CLI)

**İçin geçerlidir:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm

Kullanıcı kapsam yapılandırma dosyası veya belirtilen yapılandırma dosyasında yer alan kaynakları listesini yönetir. Kullanıcı kapsam yapılandırma dosyası şu konumdadır `%appdata%\NuGet\NuGet.Config` (Windows) ve `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Nuget.org kaynak URL'si Not `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Kullanım

```cli
nuget sources <operation> -Name <name> -Source <source>
```

Burada `<operation>` biri *listesinde, eklemek, kaldırmak, devre dışı bırakma, etkinleştirme* veya *güncelleştirme*, `<name>` kaynak adıdır ve `<source>` kaynağının URL'si. Bir kerede yalnızca bir kaynak üzerinde çalışabilir.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar. |
| Biçimi | Uygulandığı `list` eylem ve `Detailed` (varsayılan) veya `Short`. |
| Help | Bilgi komut için yardımı görüntüler. |
| NonInteractive | Kullanıcı girişini veya onaylar ister bastırır. |
| Parola | Kaynak kimliğini doğrulamak için parolayı belirtir. |
| StorePasswordInClearText | Varsayılan davranışını şifrelenmiş biçimde depolamak yerine şifrelenmemiş metin parolayı depolamak için gösterir. |
| UserName | Kaynak ile kimlik doğrulaması için kullanıcı adını belirtir. |
| Verbosity | Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

> [!Note]
> Nuget.exe daha sonra paket kaynağına erişmek için kullanılan aynı kullanıcı bağlamı altında da kaynaklarının parola eklediğinizden emin olun. Parola yapılandırma dosyasında şifrelenen depolanır ve bu şifrelenmiş olarak yalnızca aynı kullanıcı bağlamında şifresi çözülebilir. Örneğin bir yapı sunucusunda yapı sunucusunu görevi altında çalıştırılacağı Windows kullanıcıyla parolanın şifrelenmesi NuGet paketlerini geri yüklemek için kullandığınızda.

Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
