---
title: NuGet CLı güncelleştirme komutu
description: nuget.exe Update komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 84f939188ac190f6d539f8ee2b422049a274f178
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622583"
---
# <a name="update-command-nuget-cli"></a>Update komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** tümü

Projedeki tüm paketleri (kullanarak `packages.config` ) en son kullanılabilir sürümlerine güncelleştirir. Çalıştırılmadan önce [' Restore '](cli-ref-restore.md) çalıştırmak önerilir `update` . (Tek bir paketi güncelleştirmek için, [`nuget install`](cli-ref-install.md) sürüm numarası belirtmeden kullanın, bu durumda NuGet en son sürümü yüklerse.)

Not: `update` Mono (Mac OSX veya Linux) altında çalışan CLI ile veya PackageReference biçimi kullanılırken çalışmaz.

`update`Bu başvurular zaten mevcut olduğundan, komut proje dosyasındaki derleme başvurularını da güncelleştirir. Güncelleştirilmiş bir pakette eklenen bir derleme varsa, yeni bir *başvuru eklenmez.* Yeni paket bağımlılıklarına Ayrıca, derleme başvuruları da eklenmez. Bu işlemleri bir güncelleştirmenin parçası olarak dahil etmek için, Paket Yöneticisi Kullanıcı arabirimini veya paket Yöneticisi konsolunu kullanarak Visual Studio 'da paketi güncelleştirin.

Bu komut, *-self* bayrağını kullanarak nuget.exe kendisini güncelleştirmek için de kullanılabilir.

## <a name="usage"></a>Kullanım

```cli
nuget update <configPath> [options]
```

`<configPath>` `packages.config` , projenin bağımlılıklarını listeleyen bir veya çözüm dosyası tanımlar.

## <a name="options"></a>Seçenekler

- **`-ConfigFile`**

  Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  Bir paketten bir dosya hedef projede zaten mevcut olduğunda varsayılan eylemi belirtir. `Overwrite`Dosyaları her zaman üzerine yazacak şekilde ayarlayın. `Ignore`Dosyaları atlamak için olarak ayarlayın.

  `PromptUser`Varsayılan olarak, bu eylem, `OverwriteAll` `IgnoreAll` kalan tüm dosyalar için uygulanacak olan veya sağlanmazsa her çakışan dosya için istemde bulunur.

- **`-ForceEnglishOutput`**

  *(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.

- **`-?|-help`**

  Komut için yardım bilgilerini görüntüler.

- **`-Id`**

  Güncelleştirilecek paket kimliklerinin bir listesini belirtir.

- **`-MSBuildPath`**

  *(4.0 +)* Komutuyla birlikte kullanılacak MSBuild 'in yolunu belirtir `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 +)* Bu komutla kullanılacak MSBuild sürümünü belirtir. Desteklenen değerler şunlardır 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Varsayılan olarak, yolunuzda MSBuild çekilir, aksi takdirde en yüksek MSBuild 'in yüklü sürümü varsayılan olarak ayarlanır.

- **`-NonInteractive`**

  Kullanıcı girişi veya onayları için istemleri bastırır.

- **`-PreRelease`**

  Yayın öncesi sürümlere güncelleştirme yapılmasına izin verir. Zaten yüklü olan ön sürüm paketleri güncelleştirilirken bu bayrak gerekli değildir.

- **`-RepositoryPath`**

  Paketlerin yüklendiği yerel klasörü belirtir.

- **`-Safe`**

  Yüklü paket ile aynı ana ve alt sürüm içinde yalnızca en yüksek sürüme sahip güncelleştirmelerin yükleneceğini belirtir.

- **`-Self`**

  En son sürüme nuget.exe güncelleştirmeler; diğer tüm bağımsız değişkenler yoksayılır.

- **`-Source`**

  Güncelleştirmeler için kullanılacak paket kaynaklarının (URL 'Ler olarak) listesini belirtir. Atlanırsa, komut yapılandırma dosyalarında belirtilen kaynakları kullanır, bkz. [ortak NuGet yapılandırmaları](../../consume-packages/configuring-nuget-behavior.md).

- **`-Verbosity [normal|quiet|detailed]`**

  Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .

- **`-Version`**

  Tek bir paket KIMLIĞIYLE birlikte kullanıldığında, güncelleştirilecek paketin sürümünü belirtir.

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
