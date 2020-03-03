---
title: NuGet CLı geri yükleme komutu
description: NuGet. exe restore komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d1768a741e3f1c48e94d854fa7d365ebfa3513ea
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231155"
---
# <a name="restore-command-nuget-cli"></a>restore komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi **Desteklenen sürümler &bullet;:** 2.7 +

`packages` klasöründe eksik olan paketleri indirir ve yükler. NuGet 4.0 + ve PackageReference biçimiyle kullanıldığında, gerekirse `obj` klasöründe bir `<project>.nuget.props` dosyası oluşturur. (Dosya kaynak denetiminden atlanabilir.)

Mac OSX ve Linux 'ta, mono üzerinde CLı ile, paketleri geri yükleme, PackageReference ile desteklenmez.

## <a name="usage"></a>Kullanım

```cli
nuget restore <projectPath> [options]
```

Burada `<projectPath>` bir çözümün veya bir `packages.config` dosyasının konumunu belirtir. Davranış ayrıntıları [için aşağıdaki açıklamalara](#remarks) bakın.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| DirectDownload | *(4.0 +)* Herhangi bir ikili dosya veya meta veri ile önbellekleri doldurmadan paketleri doğrudan indirir. |
| DisableParallelProcessing | Birden çok paketin paralel olarak geri yüklenmesini devre dışı bırakır. |
| FallbackSource | *(3.2 +)* Paketin birincil veya varsayılan kaynakta bulunamaması durumunda fallyedekler olarak kullanılacak paket kaynaklarının bir listesi. Liste girdilerini ayırmak için noktalı virgül kullanın. |
| Zorla | PackageReference tabanlı projelerde, son geri yükleme başarılı olsa bile tüm bağımlılıkların çözülmesini zorlar. Bu bayrağın belirtilmesi `project.assets.json` dosyasını silmeye benzerdir. Bu, http-cache ' i atlar. |
| ForceEnglishOutput | *(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Forcedeğerlendir | Bir kilit dosyası zaten mevcut olsa bile, geri yüklemeyi tüm bağımlılıklara yeniden değerlendirmeye zorlar. |
| Yardım | Komut için yardım bilgilerini görüntüler. |
| LockFilePath | Proje kilit dosyasının yazıldığı çıkış konumu. Bu, varsayılan olarak ' PROJECT_ROOT \packages.Lock.json ' olur. |
| LockedMode | Proje kilit dosyası güncelleştirilmeye izin verme. |
| MSBuildPath | *(4.0 +)* Komutuyla kullanılacak MSBuild 'in yolunu belirtir ve `-MSBuildVersion`göre önceliklidir. |
| MSBuildVersion | *(3.2 +)* Bu komutla kullanılacak MSBuild sürümünü belirtir. Desteklenen değerler şunlardır 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Varsayılan olarak, yolunuzda MSBuild çekilir, aksi takdirde en yüksek MSBuild 'in yüklü sürümü varsayılan olarak ayarlanır. |
| NoCache | NuGet 'in önbelleğe alınmış paketleri kullanmasını engeller. Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Kullanıcı girişi veya onayları için istemleri bastırır. |
| OutputDirectory | Paketlerin yüklendiği klasörü belirtir. Hiçbir klasör belirtilmemişse, geçerli klasör kullanılır. `PackagesDirectory` veya `SolutionDirectory` kullanılmadığı takdirde bir `packages.config` dosyası ile geri yüklenirken gereklidir.|
| PackageSaveMode | Paket yüklemesinden sonra kaydedilecek dosya türlerini belirtir: bir `nuspec`, `nupkg`veya `nuspec;nupkg`. |
| PackagesDirectory | `OutputDirectory`ile aynı. `OutputDirectory` veya `SolutionDirectory` kullanılmadığı takdirde bir `packages.config` dosyası ile geri yüklenirken gereklidir. |
| Project2ProjectTimeOut | Projeden projeye başvuruları çözümlemek için saniye cinsinden zaman aşımı. |
| özyinelemeli | *(4.0 +)* UWP ve .NET Core projeleri için tüm başvuru projelerini geri yükler. `packages.config`kullanan projelere uygulanmaz. |
| Requireonayı | Paketleri indirmeden ve yüklemeden önce paketlerin geri yükleme işleminin etkinleştirildiğini doğrular. Ayrıntılar için bkz. [paket geri yükleme](../../consume-packages/package-restore.md). |
| SolutionDirectory | Çözüm klasörünü belirtir. Bir çözümün paketleri geri yüklenirken geçerli değildir. `PackagesDirectory` veya `OutputDirectory` kullanılmadığı takdirde bir `packages.config` dosyası ile geri yüklenirken gereklidir. |
| Kaynak | Geri yükleme için kullanılacak paket kaynaklarının (URL 'Ler olarak) listesini belirtir. Atlanırsa, komut yapılandırma dosyalarında belirtilen kaynakları kullanır, bkz. [NuGet davranışını yapılandırma](../../consume-packages/configuring-nuget-behavior.md). Liste girdilerini ayırmak için noktalı virgül kullanın. |
| UseLockFile | Proje kilitleme dosyasının oluşturulup geri yükleme ile kullanılmasını sağlar. |
| Ayrıntı Düzeyi | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="remarks"></a>Açıklamalar

Restore komutu aşağıdaki adımları gerçekleştirir:

1. Restore komutunun işlem modunu belirleme.

   | projectPath dosya türü | Davranış |
   | --- | --- |
   | Çözüm (klasör) | NuGet bir `.sln` dosyası arar ve bulursa kullanır; Aksi takdirde bir hata verir. `(SolutionDir)\.nuget` başlangıç klasörü olarak kullanılır. |
   | `.sln` dosyası | Çözüm tarafından tanımlanan paketleri geri yükleme; `-SolutionDirectory` kullanılıyorsa bir hata verir. `$(SolutionDir)\.nuget` başlangıç klasörü olarak kullanılır. |
   | `packages.config` veya proje dosyası | Dosyada listelenen paketleri geri yükleme, bağımlılıkları çözme ve yükleme. |
   | Diğer dosya türü | Dosyanın yukarıdaki gibi bir `.sln` dosyası olduğu varsayılır; bir çözüm değilse, NuGet bir hata verir. |
   | (projectPath belirtilmemiş) | <ul><li>NuGet, geçerli klasörde çözüm dosyalarını arar. Tek bir dosya bulunursa, paket geri yüklemek için kullanılır; birden çok çözüm bulunursa NuGet bir hata verir.</li><li>Çözüm dosyası yoksa, NuGet bir `packages.config` arar ve paketleri geri yüklemek için kullanır.</li><li>Hiçbir çözüm veya `packages.config` dosyası bulunamazsa, NuGet bir hata verir.</ul> |

2. Aşağıdaki öncelik sırasını kullanarak paketler klasörünü belirleme (NuGet, bu klasörlerden hiçbiri bulunmazsa bir hata verir):

    - `-PackagesDirectory`ile belirtilen klasör.
    - `Nuget.Config` `repositoryPath` değeri
    - `-SolutionDirectory` ile belirtilen klasör
    - `$(SolutionDir)\packages`

3. Bir çözümün paketlerini geri yüklerken NuGet aşağıdakileri yapar:
    - Çözüm dosyasını yükler.
    - `$(SolutionDir)\.nuget\packages.config` ' de listelenen çözüm düzeyi paketleri `packages` klasörüne geri yükler.
    - `$(ProjectDir)\packages.config` ' de listelenen paketleri `packages` klasörüne geri yükleyin. Belirtilen her paket için, `-DisableParallelProcessing` belirtilmediği takdirde paketi paralel olarak geri yükleyin.

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
