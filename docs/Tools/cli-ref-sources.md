---
title: "NuGet CLI kaynakları komut | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Komut nuget.exe için başvuru kaynakları"
keywords: "nuget başvuru kaynakları, komut kaynakları"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 139a9494e1ea898c90ce79d5990530fbe08642bd
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/15/2018
---
# <a name="sources-command-nuget-cli"></a>kaynakları komutu (NuGet CLI)

**Uygulandığı öğe:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm

Kullanıcı kapsam yapılandırma dosyası veya belirtilen yapılandırma dosyasında bulunan kaynakları listesini yönetir. Kullanıcı kapsam yapılandırma dosyası şu konumdadır `%APPDATA%\NuGet\NuGet.Config` (Windows) ve `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Nuget.org kaynak URL'sini olduğuna dikkat edin `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Kullanım

```cli
nuget sources <operation> -Name <name> -Source <source>
```

Burada `<operation>` biri *listesinde, eklemek, kaldırmak, etkinleştirme, devre dışı bırakma,* veya *güncelleştirme*, `<name>` kaynak adıdır ve `<source>` kaynağının URL'si.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Biçimi | Uygulandığı öğe `list` eylem ve `Detailed` (varsayılan) veya `Short`. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Parola | Kaynağı ile kimlik doğrulaması için parolayı belirtir. |
| StorePasswordInClearText | Şifrelenmiş biçimde depolamak varsayılan davranışını yerine şifresiz metin parolayı depolamak için gösterir. |
| UserName | Kaynağı ile kimlik doğrulaması için kullanıcı adını belirtir. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

> [!Note]
> Nuget.exe daha sonra paket kaynağına erişmek için kullanılan aynı kullanıcı bağlamında kaynakları parola eklediğinizden emin olun. Parola yapılandırma dosyasında şifrelenen depolanır ve şifrelenmiş olan gibi yalnızca aynı kullanıcı bağlamında şifresi çözülebilir. Dolayısıyla örneğin bir yapı sunucusunu aynı Windows kullanıcı derleme sunucu görevi çalıştırılacağı parola şifrelenmelidir NuGet paketlerini geri yüklemek için kullandığınızda.

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
