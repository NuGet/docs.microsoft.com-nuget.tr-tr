---
title: NuGet CLı geri yükleme komutu
description: NuGet. exe restore komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 8ba61fa87118108c36e9dc73f30d964380d02dab
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380464"
---
# <a name="restore-command-nuget-cli"></a>restore komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** 2.7 +

@No__t-0 klasöründe eksik olan paketleri indirir ve yükler. NuGet 4.0 + ve PackageReference biçimiyle kullanıldığında, gerekirse `obj` klasöründe bir `<project>.nuget.props` dosyası üretir. (Dosya kaynak denetiminden atlanabilir.)

Mac OSX ve Linux 'ta, mono üzerinde CLı ile, paketleri geri yükleme, PackageReference ile desteklenmez.

## <a name="usage"></a>Kullanım

```cli
nuget restore <projectPath> [options]
```

Burada `<projectPath>` bir çözümün veya bir `packages.config` dosyasının konumunu belirtir. Davranış ayrıntıları [için aşağıdaki açıklamalara](#remarks) bakın.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| DirectDownload | *(4.0 +)* Herhangi bir ikili dosya veya meta veri ile önbellekleri doldurmadan paketleri doğrudan indirir. |
| DisableParallelProcessing | Birden çok paketin paralel olarak geri yüklenmesini devre dışı bırakır. |
| FallbackSource | *(3.2 +)* Paketin birincil veya varsayılan kaynakta bulunamaması durumunda fallyedekler olarak kullanılacak paket kaynaklarının bir listesi. Liste girdilerini ayırmak için noktalı virgül kullanın. |
| ForceEnglishOutput | *(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Yardım | Komut için yardım bilgilerini görüntüler. |
| MSBuildPath | *(4.0 +)* @No__t-1 ' den öncelikli olarak, komutuyla kullanılacak MSBuild yolunu belirtir. |
| MSBuildVersion | *(3.2 +)* Bu komutla kullanılacak MSBuild sürümünü belirtir. Desteklenen değerler şunlardır 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Varsayılan olarak, yolunuzda MSBuild çekilir, aksi takdirde en yüksek MSBuild 'in yüklü sürümü varsayılan olarak ayarlanır. |
| NoCache | NuGet 'in önbelleğe alınmış paketleri kullanmasını engeller. Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| Etkileşimsiz | Kullanıcı girişi veya onayları için istemleri bastırır. |
| OutputDirectory | Paketlerin yüklendiği klasörü belirtir. Hiçbir klasör belirtilmemişse, geçerli klasör kullanılır. @No__t-1 veya `SolutionDirectory` kullanılmazsa `packages.config` dosyası ile geri yüklenirken gereklidir.|
| PackageSaveMode | Paket yüklemesinden sonra kaydedilecek dosya türlerini belirtir: biri `nuspec`, `nupkg` veya `nuspec;nupkg`. |
| PackagesDirectory | @No__t-0 ile aynı. @No__t-1 veya `SolutionDirectory` kullanılmazsa `packages.config` dosyası ile geri yüklenirken gereklidir. |
| Project2ProjectTimeOut | Projeden projeye başvuruları çözümlemek için saniye cinsinden zaman aşımı. |
| öz | *(4.0 +)* UWP ve .NET Core projeleri için tüm başvuru projelerini geri yükler. @No__t-0 kullanılarak projeler için uygulanmaz. |
| Requireonayı | Paketleri indirmeden ve yüklemeden önce paketlerin geri yükleme işleminin etkinleştirildiğini doğrular. Ayrıntılar için bkz. [paket geri yükleme](../../consume-packages/package-restore.md). |
| SolutionDirectory | Çözüm klasörünü belirtir. Bir çözümün paketleri geri yüklenirken geçerli değildir. @No__t-1 veya `OutputDirectory` kullanılmazsa `packages.config` dosyası ile geri yüklenirken gereklidir. |
| Kaynak | Geri yükleme için kullanılacak paket kaynaklarının (URL 'Ler olarak) listesini belirtir. Atlanırsa, komut yapılandırma dosyalarında belirtilen kaynakları kullanır, bkz. [NuGet davranışını yapılandırma](../../consume-packages/configuring-nuget-behavior.md). Liste girdilerini ayırmak için noktalı virgül kullanın. |
| Zorla | PackageReference tabanlı projelerde, son geri yükleme başarılı olsa bile tüm bağımlılıkların çözülmesini zorlar. Bu bayrağın belirtilmesi `project.assets.json` dosyasını silmeye benzerdir. Bu, http-cache ' i atlar. |
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
   | (projectPath belirtilmemiş) | <ul><li>NuGet, geçerli klasörde çözüm dosyalarını arar. Tek bir dosya bulunursa, paket geri yüklemek için kullanılır; birden çok çözüm bulunursa NuGet bir hata verir.</li><li>Çözüm dosyası yoksa, NuGet bir `packages.config` arar ve paketleri geri yüklemek için kullanır.</li><li>Çözüm yoksa veya `packages.config` dosyası bulunamazsa, NuGet bir hata verir.</ul> |

2. Aşağıdaki öncelik sırasını kullanarak paketler klasörünü belirleme (NuGet, bu klasörlerden hiçbiri bulunmazsa bir hata verir):

    - @No__t-0 ile belirtilen klasör.
    - @No__t-1 ' deki `repositoryPath` değeri
    - @No__t ile belirtilen klasör-0
    - `$(SolutionDir)\packages`

3. Bir çözümün paketlerini geri yüklerken NuGet aşağıdakileri yapar:
    - Çözüm dosyasını yükler.
    - @No__t-0 ' da listelenen çözüm düzeyi paketleri `packages` klasörüne geri yükler.
    - @No__t-0 ' da listelenen paketleri `packages` klasörüne geri yükleyin. Belirtilen her paket için `-DisableParallelProcessing` belirtilmedikçe paketi paralel olarak geri yükleyin.

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
