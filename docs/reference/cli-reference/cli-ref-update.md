---
title: NuGet CLı güncelleştirme komutu
description: NuGet. exe Update komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328257"
---
# <a name="update-command-nuget-cli"></a>Update komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** tümü

Projedeki tüm paketleri (kullanarak `packages.config`) en son kullanılabilir sürümlerine güncelleştirir. Çalıştırılmadan önce `update` [' Restore '](cli-ref-restore.md) çalıştırmak önerilir. (Tek bir paketi güncelleştirmek için, sürüm [`nuget install`](cli-ref-install.md) numarası belirtmeden kullanın, bu durumda NuGet en son sürümü yüklerse.)

Not: `update` Mono (Mac OSX veya Linux) altında çalışan CLI ile veya packagereference biçimi kullanılırken çalışmaz.

Bu başvurular zaten mevcut olduğundan, komutprojedosyasındakiderlemebaşvurularınıdagüncelleştirir.`update` Güncelleştirilmiş bir pakette eklenen bir derleme varsa, yeni bir *başvuru eklenmez.* Yeni paket bağımlılıklarına Ayrıca, derleme başvuruları da eklenmez. Bu işlemleri bir güncelleştirmenin parçası olarak dahil etmek için, Paket Yöneticisi Kullanıcı arabirimini veya paket Yöneticisi konsolunu kullanarak Visual Studio 'da paketi güncelleştirin.

Bu komut, *-self* bayrağını kullanarak NuGet. exe ' yi güncelleştirmek için de kullanılabilir.

## <a name="usage"></a>Kullanım

```cli
nuget update <configPath> [options]
```

, projenin bağımlılıklarını listeleyen `packages.config` bir veya çözüm dosyası tanımlar.`<configPath>`

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| FileConflictAction | Proje tarafından başvurulan var olan dosyaların üzerine yazılması veya yoksayılması istendiğinde gerçekleştirilecek eylemi belirtir. Değerler *üzerine yazılır, yok say, yok*. |
| ForceEnglishOutput | *(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Help | Komut için yardım bilgilerini görüntüler. |
| Id | Güncelleştirilecek paket kimliklerinin bir listesini belirtir. |
| MSBuildPath | *(4.0 +)* Komutuyla birlikte kullanılacak MSBuild 'in yolunu belirtir `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)* Bu komutla kullanılacak MSBuild sürümünü belirtir. Desteklenen değerler şunlardır 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Varsayılan olarak, yolunuzda MSBuild çekilir, aksi takdirde en yüksek MSBuild 'in yüklü sürümü varsayılan olarak ayarlanır. |
| NonInteractive | Kullanıcı girişi veya onayları için istemleri bastırır. |
| Sp1'in | Yayın öncesi sürümlere güncelleştirme yapılmasına izin verir. Zaten yüklü olan ön sürüm paketleri güncelleştirilirken bu bayrak gerekli değildir. |
| RepositoryPath | Paketlerin yüklendiği yerel klasörü belirtir. |
| Güven | Yüklü paket ile aynı ana ve alt sürüm içinde yalnızca en yüksek sürüme sahip güncelleştirmelerin yükleneceğini belirtir. |
| Self | NuGet. exe ' yi en son sürüme güncelleştirir; diğer tüm bağımsız değişkenler yoksayılır. |
| Source | Güncelleştirmeler için kullanılacak paket kaynaklarının (URL 'Ler olarak) listesini belirtir. Atlanırsa, komut yapılandırma dosyalarında belirtilen kaynakları kullanır, bkz. [ortak NuGet yapılandırmaları](../../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |
| Sürüm | Tek bir paket KIMLIĞIYLE birlikte kullanıldığında, güncelleştirilecek paketin sürümünü belirtir. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
