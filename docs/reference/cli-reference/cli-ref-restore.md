---
title: NuGet CLı geri yükleme komutu
description: nuget.exe restore komutu için başvuru
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 49fabbd0ef0c1c0c16f13bdf741296575fa72359
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780030"
---
# <a name="restore-command-nuget-cli"></a>restore komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** 2.7 +

Klasörde eksik olan paketleri indirir ve yükler `packages` . NuGet 4.0 + ve PackageReference biçimiyle kullanıldığında, `<project>.nuget.props` klasörde, gerekirse bir dosya oluşturur `obj` . (Dosya kaynak denetiminden atlanabilir.)

Mac OSX ve Linux 'ta, mono üzerinde CLı ile, paketleri geri yükleme, PackageReference ile desteklenmez.

## <a name="usage"></a>Kullanım

```cli
nuget restore <projectPath> [options]
```

`<projectPath>`bir çözümün veya dosyanın konumunu belirtir `packages.config` . Davranış ayrıntıları [için aşağıdaki açıklamalara](#remarks) bakın.

## <a name="options"></a>Seçenekler

- **`-ConfigFile`**

  Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.

- **`-DirectDownload`**

  *(4.0 +)* Herhangi bir ikili dosya veya meta veri ile önbellekleri doldurmadan paketleri doğrudan indirir.

- **`-DisableParallelProcessing`**

   Birden çok paketin paralel olarak geri yüklenmesini devre dışı bırakır.

- **`-FallbackSource`**

  *(3.2 +)* Paketin birincil veya varsayılan kaynakta bulunamaması durumunda fallyedekler olarak kullanılacak paket kaynaklarının bir listesi. Liste girdilerini ayırmak için noktalı virgül kullanın.

- **`-Force`**

  PackageReference tabanlı projelerde, son geri yükleme başarılı olsa bile tüm bağımlılıkların çözülmesini zorlar. Bu bayrağın belirtilmesi, dosyanın silinmesine benzer `project.assets.json` . Bu, http-cache ' i atlar.

- **`-ForceEnglishOutput`**

  *(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.

- **`-ForceEvaluate`**

  Bir kilit dosyası zaten mevcut olsa bile, geri yüklemeyi tüm bağımlılıklara yeniden değerlendirmeye zorlar.

- **`-?|-help`**

  Komut için yardım bilgilerini görüntüler.

- **`-LockFilePath`**

  Proje kilit dosyasının yazıldığı çıkış konumu. Bu, varsayılan olarak `PROJECT_ROOT\packages.lock.json` .

- **`-LockedMode`**

  Proje kilit dosyası güncelleştirilmeye izin verme.

- **`-MSBuildPath`**

   *(4.0 +)* Komutuyla birlikte kullanılacak MSBuild 'in yolunu belirtir `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 +)* Bu komutla kullanılacak MSBuild sürümünü belirtir. Desteklenen değerler şunlardır 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Varsayılan olarak, yolunuzda MSBuild çekilir, aksi takdirde en yüksek MSBuild 'in yüklü sürümü varsayılan olarak ayarlanır.

- **`-NoCache`**

  NuGet 'in önbelleğe alınmış paketleri kullanmasını engeller. Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-NonInteractive`**

  Kullanıcı girişi veya onayları için istemleri bastırır.

- **`-OutputDirectory`**

  Paketlerin yüklendiği klasörü belirtir. Hiçbir klasör belirtilmemişse, geçerli klasör kullanılır. `packages.config` `PackagesDirectory` Veya kullanılmamışsa bir dosyayla geri yüklenirken gereklidir `SolutionDirectory` .

- **`-PackageSaveMode`**

  Paket yüklemesinden sonra kaydedilecek dosya türlerini belirtir: `nuspec` ,, `nupkg` veya `nuspec;nupkg` .

- **`-PackagesDirectory`**

  Aynı `OutputDirectory` . `packages.config` `OutputDirectory` Veya kullanılmamışsa bir dosyayla geri yüklenirken gereklidir `SolutionDirectory` .

- **`-Project2ProjectTimeOut`**

  Projeden projeye başvuruları çözümlemek için saniye cinsinden zaman aşımı.

- **`-Recursive`**

  *(4.0 +)* UWP ve .NET Core projeleri için tüm başvuru projelerini geri yükler. Kullanılarak projeler için geçerlidir `packages.config` .

- **`-RequireConsent`**

  Paketleri indirmeden ve yüklemeden önce paketlerin geri yükleme işleminin etkinleştirildiğini doğrular. Ayrıntılar için bkz. [paket geri yükleme](../../consume-packages/package-restore.md).

- **`-SolutionDirectory`**

  Çözüm klasörünü belirtir. Bir çözümün paketleri geri yüklenirken geçerli değildir. `packages.config` `PackagesDirectory` Veya kullanılmamışsa bir dosyayla geri yüklenirken gereklidir `OutputDirectory` .

- **`-Source`**

  Geri yükleme için kullanılacak paket kaynaklarının (URL 'Ler olarak) listesini belirtir. Atlanırsa, komut yapılandırma dosyalarında belirtilen kaynakları kullanır, bkz. [NuGet davranışını yapılandırma](../../consume-packages/configuring-nuget-behavior.md). Liste girdilerini ayırmak için noktalı virgül kullanın.

- **`-UseLockFile`**

  Proje kilitleme dosyasının oluşturulup geri yükleme ile kullanılmasını sağlar.

- **`-Verbosity [normal|quiet|detailed]`**

  Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="remarks"></a>Açıklamalar

Restore komutu aşağıdaki adımları gerçekleştirir:

1. Restore komutunun işlem modunu belirleme.

   | projectPath dosya türü | Davranış |
   | --- | --- |
   | Çözüm (klasör) | NuGet bir dosya arar `.sln` ve bulursa kullanır; Aksi takdirde bir hata verir. `(SolutionDir)\.nuget` başlangıç klasörü olarak kullanılır. |
   | `.sln` dosyasýný | Çözüm tarafından tanımlanan paketleri geri yükleme; kullanılıyorsa bir hata verir `-SolutionDirectory` . `$(SolutionDir)\.nuget` başlangıç klasörü olarak kullanılır. |
   | `packages.config` veya proje dosyası | Dosyada listelenen paketleri geri yükleme, bağımlılıkları çözme ve yükleme. |
   | Diğer dosya türü | Dosyanın `.sln` yukarıdaki gibi bir dosya olduğu varsayılır; bir çözüm değilse, NuGet bir hata verir. |
   | (projectPath belirtilmemiş) | <ul><li>NuGet, geçerli klasörde çözüm dosyalarını arar. Tek bir dosya bulunursa, paket geri yüklemek için kullanılır; birden çok çözüm bulunursa NuGet bir hata verir.</li><li>Çözüm dosyası yoksa, NuGet bir arar `packages.config` ve paketleri geri yüklemek için kullanır.</li><li>Çözüm veya `packages.config` Dosya bulunamazsa, NuGet bir hata verir.</ul> |

2. Aşağıdaki öncelik sırasını kullanarak paketler klasörünü belirleme (NuGet, bu klasörlerden hiçbiri bulunmazsa bir hata verir):

    - İle belirtilen klasör `-PackagesDirectory` .
    - `repositoryPath`İçindeki değer`Nuget.Config`
    - İle belirtilen klasör `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Bir çözümün paketlerini geri yüklerken NuGet aşağıdakileri yapar:
    - Çözüm dosyasını yükler.
    - İçinde listelenen çözüm düzeyi paketleri `$(SolutionDir)\.nuget\packages.config` klasörüne geri yükler `packages` .
    - İçinde listelenen paketleri `$(ProjectDir)\packages.config` klasörüne geri yükleyin `packages` . Belirtilen her paket için, belirtilmediği takdirde paketi paralel olarak geri yükleyin `-DisableParallelProcessing` .

## <a name="examples"></a>Örnekler

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
