---
title: NuGet CLI güncelleştirme komutu
description: Nuget.exe güncelleştirme komut başvurusu
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a242d02a54fd86899cbe274ab63538b53307c1bb
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425915"
---
# <a name="update-command-nuget-cli"></a>Güncelleştirme komut (NuGet CLI)

**İçin geçerlidir:** paketini tüketim &bullet; **desteklenen sürümler:** tüm

Güncelleştirmeleri bir projedeki tüm paketleri (kullanarak `packages.config`), en son kullanılabilir sürümler için. Çalıştırmak için önerilen ['restore'](cli-ref-restore.md) çalıştırmadan önce `update`. (Tek bir paket güncelleştirmek için [ `nuget install` ](cli-ref-install.md) büyük/küçük harf NuGet en son sürümünü yükler, bir sürüm numarası belirtmeden.)

Not: `update` Mono (Mac OSX veya Linux) altında veya PackageReference biçimi kullanılırken çalıştıran CLI ile çalışmaz.

`update` Komut proje dosyasındaki derleme başvurularını de güncelleştirir, bu başvuruları sağlanan zaten mevcut. Güncelleştirilmiş bir paket eklenen bir derleme varsa, yeni bir başvurudur *değil* eklendi. Yeni paket bağımlılıkları da derleme başvurularını eklenen yok. Bu işlemler, bir güncelleştirmenin bir parçası dahil etmek için Visual Studio'da Paket Yöneticisi UI veya Paket Yöneticisi konsolu kullanarak paket güncelleştirin.

Bu komut ayrıca nuget.exe kendisini güncelleştirmek için kullanılabilir kullanarak *-kendi kendine* bayrağı.

## <a name="usage"></a>Kullanım

```cli
nuget update <configPath> [options]
```

Burada `<configPath>` ya da tanımlayan bir `packages.config` veya çözüm dosyası, proje bağımlılıkları listeler.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| FileConflictAction | Üzerine ya da proje tarafından başvurulan mevcut dosyaları yoksaymak için sorulduğunda gerçekleştirilecek eylemi belirtir. Değerler *üzerine, Ignore hiçbiri*. |
| ForceEnglishOutput | *(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar. |
| Help | Bilgi komut için yardımı görüntüler. |
| Id | Paketi güncelleştirmeye kimlikleri listesini belirtir. |
| MSBuildPath | *(4.0 +)*  Önceliği alma komutu ile kullanılacak MSBuild yolunu belirtir `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Bu komutla birlikte kullanılacak MSBuild sürümünü belirtir. Desteklenen değerler şunlardır: 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15,8, 15.9. Yolunuza Msbuild'de çekilir varsayılan olarak, aksi takdirde MSBuild yüksek yüklü sürümü varsayar. |
| NonInteractive | Kullanıcı girişini veya onaylar ister bastırır. |
| Yayın öncesi | Yayın öncesi sürümler için güncelleştirme sağlar. Bu bayrak, zaten yüklü olan yayın öncesi paketleri güncelleştirirken gerekli değildir. |
| Dosyasının repositorypath ayarı | Paket yüklendiği yerel klasörü belirtir. |
| Güvenli | Yüklü paketleri yüklü olarak, yalnızca aynı birincil ve ikincil sürüm içinde mevcut olan en yüksek sürüm güncelleştirir belirtir. |
| Kendi kendine | En son sürüme güncelleştirme nuget.exe; diğer tüm bağımsız değişkenler yoksayılır. |
| Source | Paket kaynaklarının listesi güncelleştirmeleri için kullanılacak (URL'ler) belirtir. Atlanırsa, komut yapılandırma dosyalarında sağlanan kaynakları kullanır, bkz: [ortak NuGet yapılandırmaları](../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |
| Sürüm | Bir paket kimliği ile kullanıldığında, güncelleştirilecek paket sürümünü belirtir. |

Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
