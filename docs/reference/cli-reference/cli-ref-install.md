---
title: NuGet CLı install komutu
description: NuGet. exe install komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f39bcc67c5f659f05ef02f2579bcf07b4481bb27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328341"
---
# <a name="install-command-nuget-cli"></a>Install komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** tümü

Belirtilen paket kaynaklarını kullanarak bir paketi indirir ve geçerli klasörü varsayılan olarak bir projeye yükler.

> [!Tip]
> Bir paketi doğrudan bir proje bağlamı dışında indirmek için, [NuGet.org](https://www.nuget.org) adresindeki paketin sayfasını ziyaret edin ve **indirme** bağlantısını seçin.

Hiçbir kaynak belirtilmemişse, genel yapılandırma dosyasında `%appdata%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) listelenenler kullanılır. Daha fazla bilgi için bkz. [ortak NuGet yapılandırması](../../consume-packages/configuring-nuget-behavior.md) .

Belirli bir paket belirtilmemişse, `install` `packages.config` projenin dosyasında listelenen tüm paketleri [`restore`](cli-ref-restore.md)' a benzer hale getirir.

Komut `install` , bir proje dosyası veya `packages.config`; bu `restore` şekilde, yalnızca paketleri diske eklemektedir ancak projenin bağımlılıklarını değiştirmediğinden buna benzer.

Bir bağımlılık eklemek için, Visual Studio 'da Paket Yöneticisi Kullanıcı arabirimi veya konsolundan bir paket ekleyin ya da `packages.config` `install` veya öğesini değiştirip veya `restore`çalıştırın.

## <a name="usage"></a>Kullanım

```cli
nuget install <packageID | configFilePath> [options]
```

, Yüklenecek paketin `<configFilePath>` `packages.config` adını (en son sürümü kullanarak) veya yüklenecek paketleri listeleyen dosyayı tanımlar. `<packageID>` `-Version` Seçeneğiyle belirli bir sürümü belirtebilirsiniz.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| DependencyVersion | *(4.4 +)* Kullanılacak bağımlılık paketlerinin sürümü, bu, aşağıdakilerden biri olabilir:<br/><ul><li>*En düşük* (varsayılan): en düşük sürüm</li><li>*HighestPatch*: en düşük ana, en düşük ikincil, en yüksek düzeltme eki olan sürüm</li><li>*HighestMinor*: en düşük ana, en yüksek ikincil, en yüksek düzeltme eki olan sürüm</li><li>*En yüksek*: en yüksek sürüm</li></ul> |
| DisableParallelProcessing | Birden çok paketi paralel olarak yüklemeyi devre dışı bırakır. |
| ExcludeVersion | Paketi, sürüm numarasını değil yalnızca paket adı ile adlandırılan bir klasöre yüklenir. |
| FallbackSource | *(3.2 +)* Paketin birincil veya varsayılan kaynakta bulunamaması durumunda fallyedekler olarak kullanılacak paket kaynaklarının bir listesi. |
| ForceEnglishOutput | *(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Framework | *(4.4 +)* Bağımlılıkları seçmek için kullanılan hedef çerçeve. Belirtilmemişse, varsayılan olarak ' any ' olur. |
| Help | Komut için yardım bilgilerini görüntüler. |
| NoCache | NuGet 'in önbelleğe alınmış paketleri kullanmasını engeller. Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Kullanıcı girişi veya onayları için istemleri bastırır. |
| OutputDirectory | Paketlerin yüklendiği klasörü belirtir. Hiçbir klasör belirtilmemişse, geçerli klasör kullanılır. |
| PackageSaveMode | Paket yüklemesinden sonra kaydedilecek dosya türlerini belirtir: `nuspec`, `nupkg`, veya `nuspec;nupkg`. |
| Sp1'in | Ön sürüm paketlerinin yüklenmesine izin verir. Paketleri ile `packages.config`geri yüklenirken bu bayrak gerekli değildir. |
| Requireonayı | Paketleri indirmeden ve yüklemeden önce paketlerin geri yükleme işleminin etkinleştirildiğini doğrular. Ayrıntılar için bkz. [paket geri yükleme](../../consume-packages/package-restore.md). |
| SolutionDirectory | Paketlerin geri yükleneceği çözümün kök klasörünü belirtir. |
| Source | Kullanılacak paket kaynaklarının (URL 'Ler olarak) listesini belirtir. Atlanırsa, komut yapılandırma dosyalarında belirtilen kaynakları kullanır, bkz. [ortak NuGet yapılandırmaları](../../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |
| Sürüm | Yüklenecek paketin sürümünü belirtir. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
