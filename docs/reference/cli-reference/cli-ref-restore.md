---
title: NuGet CLı geri yükleme komutu
description: NuGet. exe restore komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 211f24ff67c06da00d6a014e679cc422d493d6d5
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959738"
---
# <a name="restore-command-nuget-cli"></a>restore komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** 2.7+

`packages` Klasörde eksik olan paketleri indirir ve yükler. NuGet 4.0 + ve packagereference biçimiyle kullanıldığında, `<project>.nuget.props` `obj` klasörde, gerekirse bir dosya oluşturur. (Dosya kaynak denetiminden atlanabilir.)

Mac OSX ve Linux 'ta, mono üzerinde CLı ile, paketleri geri yükleme, PackageReference ile desteklenmez.

## <a name="usage"></a>Kullanım

```cli
nuget restore <projectPath> [options]
```

bir çözümün`packages.config` veya dosyanın konumunu belirtir.`<projectPath>` Davranış [](#remarks) ayrıntıları için aşağıdaki açıklamalara bakın.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| DirectDownload | *(4.0 +)* Herhangi bir ikili dosya veya meta veri ile önbellekleri doldurmadan paketleri doğrudan indirir. |
| DisableParallelProcessing | Birden çok paketin paralel olarak geri yüklenmesini devre dışı bırakır. |
| FallbackSource | *(3.2 +)* Paketin birincil veya varsayılan kaynakta bulunamaması durumunda fallyedekler olarak kullanılacak paket kaynaklarının bir listesi. Liste girdilerini ayırmak için noktalı virgül kullanın. |
| ForceEnglishOutput | *(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Help | Komut için yardım bilgilerini görüntüler. |
| MSBuildPath | *(4.0 +)* Komutuyla birlikte kullanılacak MSBuild 'in yolunu belirtir `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)* Bu komutla kullanılacak MSBuild sürümünü belirtir. Desteklenen değerler şunlardır 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Varsayılan olarak, yolunuzda MSBuild çekilir, aksi takdirde en yüksek MSBuild 'in yüklü sürümü varsayılan olarak ayarlanır. |
| NoCache | NuGet 'in önbelleğe alınmış paketleri kullanmasını engeller. Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Kullanıcı girişi veya onayları için istemleri bastırır. |
| OutputDirectory | Paketlerin yüklendiği klasörü belirtir. Hiçbir klasör belirtilmemişse, geçerli klasör kullanılır. Veya `packages.config` `PackagesDirectory` kullanılmamışsa bir dosyayla geri yüklenirken gereklidir. `SolutionDirectory`|
| PackageSaveMode | Paket yüklemesinden sonra kaydedilecek dosya türlerini belirtir: `nuspec`, `nupkg`, veya `nuspec;nupkg`. |
| PackagesDirectory | `OutputDirectory`Aynı. Veya `packages.config` `OutputDirectory` kullanılmamışsa bir dosyayla geri yüklenirken gereklidir. `SolutionDirectory` |
| Project2ProjectTimeOut | Projeden projeye başvuruları çözümlemek için saniye cinsinden zaman aşımı. |
| özyinelemeli | *(4.0 +)* UWP ve .NET Core projeleri için tüm başvuru projelerini geri yükler. Kullanılarak `packages.config`projeler için geçerlidir. |
| Requireonayı | Paketleri indirmeden ve yüklemeden önce paketlerin geri yükleme işleminin etkinleştirildiğini doğrular. Ayrıntılar için bkz. [paket geri yükleme](../../consume-packages/package-restore.md). |
| SolutionDirectory | Çözüm klasörünü belirtir. Bir çözümün paketleri geri yüklenirken geçerli değildir. Veya `packages.config` `PackagesDirectory` kullanılmamışsa bir dosyayla geri yüklenirken gereklidir. `OutputDirectory` |
| Source | Geri yükleme için kullanılacak paket kaynaklarının (URL 'Ler olarak) listesini belirtir. Atlanırsa, komut yapılandırma dosyalarında belirtilen kaynakları kullanır, bkz. [NuGet davranışını yapılandırma](../../consume-packages/configuring-nuget-behavior.md). Liste girdilerini ayırmak için noktalı virgül kullanın. |
| Verbosity | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="remarks"></a>Açıklamalar

Restore komutu aşağıdaki adımları gerçekleştirir:

1. Restore komutunun işlem modunu belirleme.

   | projectPath dosya türü | Davranış |
   | --- | --- |
   | Çözüm (klasör) | NuGet bir `.sln` dosya arar ve bulursa kullanır; Aksi takdirde bir hata verir. `(SolutionDir)\.nuget`başlangıç klasörü olarak kullanılır. |
   | `.sln`dosyasýný | Çözüm tarafından tanımlanan paketleri geri yükleme; kullanılıyorsa bir hata `-SolutionDirectory` verir. `$(SolutionDir)\.nuget`başlangıç klasörü olarak kullanılır. |
   | `packages.config`veya proje dosyası | Dosyada listelenen paketleri geri yükleme, bağımlılıkları çözme ve yükleme. |
   | Diğer dosya türü | Dosyanın yukarıdaki gibi bir `.sln` dosya olduğu varsayılır; bir çözüm değilse, NuGet bir hata verir. |
   | (projectPath belirtilmemiş) | <ul><li>NuGet, geçerli klasörde çözüm dosyalarını arar. Tek bir dosya bulunursa, paket geri yüklemek için kullanılır; birden çok çözüm bulunursa NuGet bir hata verir.</li><li>Çözüm dosyası yoksa, NuGet bir `packages.config` arar ve paketleri geri yüklemek için kullanır.</li><li>Çözüm veya `packages.config` dosya bulunamazsa, NuGet bir hata verir.</ul> |

2. Aşağıdaki öncelik sırasını kullanarak paketler klasörünü belirleme (NuGet, bu klasörlerden hiçbiri bulunmazsa bir hata verir):

    - İle `-PackagesDirectory`belirtilen klasör.
    - İçindeki `repositoryPath` değer`Nuget.Config`
    - İle belirtilen klasör`-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Bir çözümün paketlerini geri yüklerken NuGet aşağıdakileri yapar:
    - Çözüm dosyasını yükler.
    - `$(SolutionDir)\.nuget\packages.config` İçinde`packages` listelenen çözüm düzeyi paketleri klasörüne geri yükler.
    - `$(ProjectDir)\packages.config` İçinde`packages` listelenen paketleri klasörüne geri yükleyin. Belirtilen her paket için, belirtilmediği takdirde `-DisableParallelProcessing` paketi paralel olarak geri yükleyin.

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
