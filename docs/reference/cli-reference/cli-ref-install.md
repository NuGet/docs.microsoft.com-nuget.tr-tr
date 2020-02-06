---
title: NuGet CLı install komutu
description: NuGet. exe install komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6c49b2406462eae6ce45c65dfd8b3a9eb1077e73
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036948"
---
# <a name="install-command-nuget-cli"></a>Install komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi **Desteklenen sürümler &bullet;:** tümü

Belirtilen paket kaynaklarını kullanarak bir paketi indirir ve geçerli klasörü varsayılan olarak bir projeye yükler.

> [!Tip]
> Bir paketi doğrudan bir proje bağlamı dışında indirmek için, [NuGet.org](https://www.nuget.org) adresindeki paketin sayfasını ziyaret edin ve **indirme** bağlantısını seçin.

Hiçbir kaynak belirtilmemişse, genel yapılandırma dosyasında listelenenler `%appdata%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır. Daha fazla bilgi için bkz. [ortak NuGet yapılandırması](../../consume-packages/configuring-nuget-behavior.md) .

Belirli bir paket belirtilmemişse, `install` projenin `packages.config` dosyasında listelenen tüm paketleri yükleyerek [`restore`](cli-ref-restore.md)benzer hale getirir.

`install` komutu bir proje dosyasını veya `packages.config`değiştirmez; Bu şekilde, yalnızca paketleri diske eklemesi, ancak projenin bağımlılıklarını değiştirmediğinden `restore` benzerdir.

Bir bağımlılık eklemek için, Visual Studio 'da Paket Yöneticisi Kullanıcı arabirimi veya konsolundan bir paket ekleyin veya `packages.config` değiştirin ve `install` ya da `restore`çalıştırın.

## <a name="usage"></a>Kullanım

```cli
nuget install <packageID | configFilePath> [options]
```

`<packageID>`, yüklenecek paketi (en son sürümü kullanarak) adlandırır veya `<configFilePath>` yüklenecek paketleri listeleyen `packages.config` dosyasını tanımlar. `-Version` seçeneği ile belirli bir sürümü belirtebilirsiniz.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| DependencyVersion | *(4.4 +)* Kullanılacak bağımlılık paketlerinin sürümü, bu, aşağıdakilerden biri olabilir:<br/><ul><li>*En düşük* (varsayılan): en düşük sürüm</li><li>*HighestPatch*: en düşük ana, en düşük ikincil, en yüksek düzeltme eki olan sürüm</li><li>*HighestMinor*: en düşük ana, en yüksek ikincil, en yüksek düzeltme eki olan sürüm</li><li>*En yüksek*: en yüksek sürüm</li><li>*Yoksay*: bağımlılık paketleri kullanılmayacak</li></ul> |
| DisableParallelProcessing | Birden çok paketi paralel olarak yüklemeyi devre dışı bırakır. |
| ExcludeVersion | Paketi, sürüm numarasını değil yalnızca paket adı ile adlandırılan bir klasöre yüklenir. |
| FallbackSource | *(3.2 +)* Paketin birincil veya varsayılan kaynakta bulunamaması durumunda fallyedekler olarak kullanılacak paket kaynaklarının bir listesi. |
| ForceEnglishOutput | *(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Framework | *(4.4 +)* Bağımlılıkları seçmek için kullanılan hedef çerçeve. Belirtilmemişse, varsayılan olarak ' any ' olur. |
| Yardım | Komut için yardım bilgilerini görüntüler. |
| NoCache | NuGet 'in önbelleğe alınmış paketleri kullanmasını engeller. Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Kullanıcı girişi veya onayları için istemleri bastırır. |
| OutputDirectory | Paketlerin yüklendiği klasörü belirtir. Hiçbir klasör belirtilmemişse, geçerli klasör kullanılır. |
| PackageSaveMode | Paket yüklemesinden sonra kaydedilecek dosya türlerini belirtir: bir `nuspec`, `nupkg`veya `nuspec;nupkg`. |
| PreRelease | Ön sürüm paketlerinin yüklenmesine izin verir. Paketler `packages.config`ile geri yüklenirken bu bayrak gerekli değildir. |
| Requireonayı | Paketleri indirmeden ve yüklemeden önce paketlerin geri yükleme işleminin etkinleştirildiğini doğrular. Ayrıntılar için bkz. [paket geri yükleme](../../consume-packages/package-restore.md). |
| SolutionDirectory | Paketlerin geri yükleneceği çözümün kök klasörünü belirtir. |
| Kaynak | Kullanılacak paket kaynaklarının (URL 'Ler olarak) listesini belirtir. Atlanırsa, komut yapılandırma dosyalarında belirtilen kaynakları kullanır, bkz. [ortak NuGet yapılandırmaları](../../consume-packages/configuring-nuget-behavior.md). |
| Ayrıntı Düzeyi | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |
| Sürüm | Yüklenecek paketin sürümünü belirtir. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
