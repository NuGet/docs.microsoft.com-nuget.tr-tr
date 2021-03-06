---
title: NuGet CLı Add komutu
description: nuget.exe Add komutu için başvuru
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 096d2f7a61a3c861ce2084368500ab8e8b21f212
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776090"
---
# <a name="add-command-nuget-cli"></a>Add komutu (NuGet CLı)

**Uygulama hedefi**: paket yayımlaması &bullet; **Desteklenen sürümler**: 3.3 +

, Paket KIMLIĞI ve sürüm numarası için klasörler içinde oluşturulan, bir hiyerarşik düzende, belirtilen bir paketi HTTP olmayan bir kaynak (klasör veya UNC yolu) öğesine ekler. Örneğin:

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

Paket kaynağına göre geri yükleme veya güncelleştirme yaparken hiyerarşik düzen önemli ölçüde daha iyi performans sağlar.

Paketteki tüm dosyaları hedef paket kaynağına genişletmek için `-Expand` anahtarını kullanın. Bu genellikle, ve gibi, hedefte görüntülenen ek alt klasörlere neden olur `tools` `lib` .

## <a name="usage"></a>Kullanım

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

, `<packagePath>` eklenecek paketin yol adı, ve `<sourcePath>` paketin ekleneceği klasör tabanlı paket kaynağını belirtir. HTTP kaynakları desteklenmez.

## <a name="options"></a>Seçenekler

- **`-ConfigFile`**

  Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.

- **`-Expand`**

  Paketteki tüm dosyaları paket kaynağına ekler.

- **`-ForceEnglishOutput`**

  *(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.
nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.

- **`-?|-help`**

  Komut için yardım bilgilerini görüntüler.

- **`-NonInteractive`**

  Kullanıcı girişi veya onayları için istemleri bastırır.

- **`-src|-Source`**

   Nupkg 'nin ekleneceği bir klasör veya UNC paylaşma olan paket kaynağını belirtir. Http kaynakları desteklenmez.

- **`-Verbosity [normal|quiet|detailed]`**

  Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
