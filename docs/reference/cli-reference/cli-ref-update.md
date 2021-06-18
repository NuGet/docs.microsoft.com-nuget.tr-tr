---
title: NuGet CLI update komutu
description: nuget.exe update komutu için başvuru
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323654"
---
# <a name="update-command-nuget-cli"></a>update komutu (NuGet CLI)

**Uygulama: paket** tüketimi &bullet; **Desteklenen sürümler:** hepsi

Bir proje içinde tüm paketleri `packages.config` (kullanarak) en son kullanılabilir sürümlerine güncelleştirme. çalıştırmadan önce ['restore' çalıştırması](cli-ref-restore.md) `update` önerilir. (Tek bir paketi güncelleştirmek için, sürüm numarası belirtmeden kullanın; bu [`nuget install`](cli-ref-install.md) durumda NuGet en son sürümü yüklüdür.)

Not: Mono (Mac OSX veya Linux) altında çalışan CLI ile veya `update` PackageReference biçimi kullanırken çalışmıyor.

Komut `update` ayrıca, bu başvuruların zaten mevcut olduğu durumda proje dosyasında derleme başvurularını da günceller. Güncelleştirilmiş bir paketin ekli bir derlemesi varsa, yeni bir *başvuru eklenmez.* Yeni paket bağımlılıklarında da derleme başvuruları eklenmez. Bu işlemleri bir güncelleştirmenin parçası olarak eklemek için Paket Yöneticisi kullanıcı arabirimini veya Visual Studio Konsolu'nu kullanarak paketi Paket Yöneticisi güncelleştirin.

Bu komut, *-self* bayrağını nuget.exe kendi kendini güncelleştirmek için de kullanılabilir.

## <a name="usage"></a>Kullanım

```cli
nuget update <configPath> [options]
```

burada, `<configPath>` projenin `packages.config` bağımlılıklarını listeleen bir veya çözüm dosyası tanımlar.

## <a name="options"></a>Seçenekler

- **`-ConfigFile`**

  Uygulanacak NuGet yapılandırma dosyası. Belirtilmezse `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  Kullanmak üzere bağımlılık paketlerinin sürümünü belirtir; bu sürüm, aşağıdakilerden biri olabilir:<br/><ul><li>*En* düşük (varsayılan): en düşük sürüm</li><li>*HighestPatch:* En düşük ana, en düşük ikincil, en yüksek düzeltme ekini olan sürüm</li><li>*HighestMinor:* en düşük ana, en yüksek ikincil, en yüksek düzeltme eki olan sürüm</li><li>*En yüksek*: en yüksek sürüm</li><li>*Yoksay:* Hiçbir bağımlılık paketi kullanılmaz</li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  Bir paketten bir dosya hedef projede zaten mevcut olduğunda varsayılan eylemi belirtir. Her zaman `Overwrite` dosyaların üzerine yaz olarak ayarlayın. Dosyaları atlamak `Ignore` için olarak ayarlayın.

  Varsayılan eylem, veya sağlanıyorsa çakışan her dosyayı ister ve bu da `PromptUser` kalan tüm dosyalar için geçerli `OverwriteAll` `IgnoreAll` olur.

- **`-ForceEnglishOutput`**

  *(3,5+)* Bu nuget.exe sabit, İngilizce tabanlı bir kültür kullanarak çalıştırmaya güçler.

- **`-?|-help`**

  Komutun yardım bilgilerini görüntüler.

- **`-Id`**

  Güncelleştirilen paket kimliklerinin listesini belirtir.

- **`-MSBuildPath`**

  *(4.0+)* komutuyla birlikte kullanmak üzere MSBuild'in yolunu belirtir ve önceliğe sahip `-MSBuildVersion` olur.

- **`-MSBuildVersion`**

  *(3.2+)* Bu komutla kullanılacak MSBuild sürümünü belirtir. Desteklenen değerler: 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9. Varsayılan olarak, yolunuz msBuild seçerek, aksi takdirde msbuild'in en yüksek yüklü sürümüne varsayılan olarak kullanılır.

- **`-NonInteractive`**

  Kullanıcı girişi veya onay istemlerini bastırıyor.

- **`-PreRelease`**

  Sürümleri ön sürüme güncelleştirmeye izin verir. Zaten yüklü olan ön sürümü paketleri güncelleştiriliyorken bu bayrak gerekli değildir.

- **`-RepositoryPath`**

  Paketlerin yüklü olduğu yerel klasörü belirtir.

- **`-Safe`**

  Yalnızca yüklü paketle aynı ana ve ikincil sürümde bulunan en yüksek sürüme sahip güncelleştirmelerin yük olacağını belirtir.

- **`-Self`**

  En `nuget.exe` son sürüme güncelleştirmeler. `-Source` kullanılabilir, ancak diğer tüm bağımsız değişkenler yoksayılır. Kaynak sağlanamıyorsa, `nuget.org` ayarlardan bağımsız olarak güncelleştirmeleri `NuGet.Config` denetler.

- **`-Source`**

  Güncelleştirmeler için kullanmak üzere paket kaynaklarının listesini (URL olarak) belirtir. Atlanırsa, komut yapılandırma dosyalarında sağlanan kaynakları kullanır, bkz. [Ortak NuGet yapılandırmaları.](../../consume-packages/configuring-nuget-behavior.md)

- **`-Verbosity [normal|quiet|detailed]`**

  Çıktıda görüntülenen ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .

- **`-Version`**

  Bir paket kimliği ile birlikte kullanılırken, güncelleştirilen paketin sürümünü belirtir.

Ayrıca [bkz. Ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
