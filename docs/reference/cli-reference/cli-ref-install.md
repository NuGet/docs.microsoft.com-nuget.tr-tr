---
title: NuGet CLı install komutu
description: nuget.exe install komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 23856728d07d07183b5aedcd6218a56a444c410b
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623103"
---
# <a name="install-command-nuget-cli"></a>Install komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** tümü

Belirtilen paket kaynaklarını kullanarak bir paketi indirir ve geçerli klasörü varsayılan olarak bir projeye yükler.

> [!Tip]
> Bir paketi doğrudan bir proje bağlamı dışında indirmek için, [NuGet.org](https://www.nuget.org) adresindeki paketin sayfasını ziyaret edin ve **indirme** bağlantısını seçin.

Hiçbir kaynak belirtilmemişse, genel yapılandırma dosyasında `%appdata%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) listelenenler kullanılır. Daha fazla bilgi için bkz. [ortak NuGet yapılandırması](../../consume-packages/configuring-nuget-behavior.md) .

Belirli bir paket belirtilmemişse, `install` projenin dosyasında listelenen tüm paketleri `packages.config` ' a benzer hale getirir [`restore`](cli-ref-restore.md) .

`install`Komut, bir proje dosyası veya `packages.config` ; Bu şekilde, `restore` yalnızca paketleri diske eklemektedir ancak projenin bağımlılıklarını değiştirmediğinden buna benzer.

Bir bağımlılık eklemek için, Visual Studio 'da Paket Yöneticisi Kullanıcı arabirimi veya konsolundan bir paket ekleyin ya da `packages.config` veya öğesini değiştirip `install` veya çalıştırın `restore` .

## <a name="usage"></a>Kullanım

```cli
nuget install <packageID | configFilePath> [options]
```

`<packageID>`, Yüklenecek paketin adını (en son sürümü kullanarak) veya `<configFilePath>` `packages.config` yüklenecek paketleri listeleyen dosyayı tanımlar. Seçeneğiyle belirli bir sürümü belirtebilirsiniz `-Version` .

## <a name="options"></a>Seçenekler

- **`-ConfigFile`**

  Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.

- **`-DependencyVersion`**

  *(4.4 +)* Kullanılacak bağımlılık paketlerinin sürümü, bu, aşağıdakilerden biri olabilir:<br/><ul><li>*En düşük* (varsayılan): en düşük sürüm</li><li>*HighestPatch*: en düşük ana, en düşük ikincil, en yüksek düzeltme eki olan sürüm</li><li>*HighestMinor*: en düşük ana, en yüksek ikincil, en yüksek düzeltme eki olan sürüm</li><li>*En yüksek*: en yüksek sürüm</li><li>*Yoksay*: bağımlılık paketleri kullanılmayacak</li></ul>

- **`-DirectDownload`**

  Meta veri veya ikili dosyaları olan herhangi bir önbelleği doldurmadan doğrudan indirin.

- **`-DisableParallelProcessing`**

  Birden çok paketi paralel olarak yüklemeyi devre dışı bırakır.

- **`-x|-ExcludeVersion`**

  Paketi, sürüm numarasını değil yalnızca paket adı ile adlandırılan bir klasöre yüklenir.

- **`-FallbackSource`**

  *(3.2 +)* Paketin birincil veya varsayılan kaynakta bulunamaması durumunda fallyedekler olarak kullanılacak paket kaynaklarının bir listesi.

- **`-ForceEnglishOutput`**

  *(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.

- **`-Framework`**

  *(4.4 +)* Bağımlılıkları seçmek için kullanılan hedef çerçeve. Belirtilmemişse, varsayılan olarak ' any ' olur.

- **`-?|-help`**

  Komut için yardım bilgilerini görüntüler.

- **`-NoCache`**

  NuGet 'in önbelleğe alınmış paketleri kullanmasını engeller. Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-NonInteractive`**

  Kullanıcı girişi veya onayları için istemleri bastırır.

- **`-OutputDirectory`**

  Paketlerin yüklendiği klasörü belirtir. Hiçbir klasör belirtilmemişse, geçerli klasör kullanılır.

- **`-PackageSaveMode`**

  Paket yüklemesinden sonra kaydedilecek dosya türlerini belirtir: `nuspec` ,, `nupkg` veya `nuspec;nupkg` .

- **`-PreRelease`**

  Ön sürüm paketlerinin yüklenmesine izin verir. Paketleri ile geri yüklenirken bu bayrak gerekli değildir `packages.config` .

- **`-RequireConsent`**

  Paketleri indirmeden ve yüklemeden önce paketlerin geri yükleme işleminin etkinleştirildiğini doğrular. Ayrıntılar için bkz. [paket geri yükleme](../../consume-packages/package-restore.md).

- **`-SolutionDirectory`**

  Paketlerin geri yükleneceği çözümün kök klasörünü belirtir.

- **`-Source`**

   Kullanılacak paket kaynaklarının (URL 'Ler olarak) listesini belirtir. Atlanırsa, komut yapılandırma dosyalarında belirtilen kaynakları kullanır, bkz. [ortak NuGet yapılandırmaları](../../consume-packages/configuring-nuget-behavior.md).

- **`-Verbosity [normal|quiet|detailed]`**

  Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .

- **`-Version`**

  Yüklenecek paketin sürümünü belirtir.

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
