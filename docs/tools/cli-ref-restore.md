---
title: CLI NuGet restore komutu
description: Nuget.exe restore komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 9964186dcbfedfbf2415a57102f8f019a1eef23a
ms.sourcegitcommit: 6b71926f062ecddb8729ef8567baf67fd269642a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59932001"
---
# <a name="restore-command-nuget-cli"></a>Restore komutu (NuGet CLI)

**İçin geçerlidir:** paketini tüketim &bullet; **desteklenen sürümler:** 2.7+

İndirir ve yükler gelen eksik herhangi bir paket `packages` klasör. NuGet 4.0 + ve PackageReference biçimi ile kullanıldığında, oluşturur bir `<project>.nuget.props` buna gerekirse dosya `obj` klasör. (Dosyanın kaynak denetiminden atlanabilir.)

Mac OSX ve Linux üzerinde Mono CLI ile paketleri geri yükleme ile PackageReference desteklenmiyor.

## <a name="usage"></a>Kullanım

```cli
nuget restore <projectPath> [options]
```

Burada `<projectPath>` çözümün konumunu belirtir veya `packages.config` dosya. Bkz: [açıklamalar](#remarks) aşağıdaki davranış Ayrıntılar için.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| DirectDownload | *(4.0 +)*  Doğrudan önbellekler herhangi bir ikili dosyaları veya meta veri ile doldurma olmadan paketleri indirir. |
| DisableParallelProcessing | Paralel birden çok paket geri yüklemeyi devre dışı bırakır. |
| FallbackSource | *(3.2 +)*  Paketi birincil bulunamadığında durumunda geri dönüşler kullanmak için paket kaynaklarının bir listesini ya da varsayılan kaynak. |
| ForceEnglishOutput | *(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar. |
| Help | Bilgi komut için yardımı görüntüler. |
| MSBuildPath | *(4.0 +)*  Önceliği alma komutu ile kullanılacak MSBuild yolunu belirtir `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Bu komutla birlikte kullanılacak MSBuild sürümünü belirtir. Desteklenen değerler şunlardır: 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15,8, 15.9. Yolunuza Msbuild'de çekilir varsayılan olarak, aksi takdirde MSBuild yüksek yüklü sürümü varsayar. |
| NoCache | NuGet, önbelleğe eklenen paketler kullanmasını önler. Bkz: [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Kullanıcı girişini veya onaylar ister bastırır. |
| OutputDirectory | Paket yüklendiği klasörünü belirtir. Klasör belirtilirse, geçerli klasörde kullanılır. İle geri yükleme sırasında gerekli bir `packages.config` sürece dosya `PackagesDirectory` veya `SolutionDirectory` kullanılır.|
| PackageSaveMode | Paket yükleme sonrasında kaydedilecek dosya türlerini belirtir: biri `nuspec`, `nupkg`, veya `nuspec;nupkg`. |
| PackagesDirectory | Aynı `OutputDirectory`. İle geri yükleme sırasında gerekli bir `packages.config` sürece dosya `OutputDirectory` veya `SolutionDirectory` kullanılır. |
| Project2ProjectTimeOut | Projeden projeye başvuruları çözümlemek için saniye cinsinden zaman aşımı. |
| özyinelemeli | *(4.0 +)*  UWP ve .NET Core projeleri için tüm başvuruları projeleri geri yükler. Kullanarak projeleri için geçerli değildir `packages.config`. |
| RequireConsent | Paketleri geri yükleme ve paketleri yüklemeden önce etkin olduğunu doğrular. Ayrıntılar için bkz [paketi geri yüklemeyi](../consume-packages/package-restore.md). |
| SolutionDirectory | Çözüm klasörü belirtir. Bir çözüm için paketler geri yüklenirken geçerli değil. İle geri yükleme sırasında gerekli bir `packages.config` sürece dosya `PackagesDirectory` veya `OutputDirectory` kullanılır. |
| Source | Paket kaynaklarının listesi, geri yüklemek için kullanılacak (URL'ler) belirtir. Atlanırsa, komut yapılandırma dosyalarında sağlanan kaynakları kullanır, bkz: [yapılandırma NuGet davranışını](../consume-packages/configuring-nuget-behavior.md). |
| Verbosity |> çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="remarks"></a>Açıklamalar

Restore komutu, aşağıdaki adımları gerçekleştirir:

1. Restore komutu, işlem modunu belirler.

   | projectPath dosya türü | Davranış |
   | --- | --- |
   | Çözüm (klasör) | NuGet arar bir `.sln` dosya ve aksi takdirde bir hata verir kullanır. `(SolutionDir)\.nuget` Başlangıç klasörü kullanılır. |
   | `.sln` Dosya | Çözüm tarafından tanımlanan paketleri geri yüklenmesi; varsa bir hata verir `-SolutionDirectory` kullanılır. `$(SolutionDir)\.nuget` Başlangıç klasörü kullanılır. |
   | `packages.config` ya da proje dosyası | Çözümleme ve Bağımlılıkların yüklenmesi dosyada listelenen paketleri geri yükleyin. |
   | Başka bir dosya türü | Dosya olduğu varsayılır bir `.sln` dosya olarak yukarıdaki; NuGet verir hata bir çözüm değilse. |
   | (belirtilmemiş projectPath) | <ul><li>NuGet, geçerli klasörde çözüm dosyalarını arar. Tek bir dosya bulunamazsa, bu paketleri geri yüklemek için kullanılır; birden fazla çözüm bulundu, NuGet bir hata verir.</li><li>Hiçbir çözüm dosyası varsa, NuGet arayan bir `packages.config` ve bu paketleri geri yüklemek için kullanır.</li><li>Hiçbir çözüm varsa veya `packages.config` dosya bulundu, NuGet bir hata verir.</ul> |

2. (Bu klasörleri hiçbiri bulunursa NuGet bir hata verir) aşağıdaki öncelik sırasını kullanarak packages klasörünü belirleyin:

    - Belirtilen klasör `-PackagesDirectory`.
    - `repositoryPath` Değeri `Nuget.Config`
    - Belirtilen klasör `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Bir çözüm için paketler geri yüklerken, NuGet şunları yapar:
    - Çözüm dosyası yükler.
    - Listelenen çözüm düzeyinde paketleri geri yükler `$(SolutionDir)\.nuget\packages.config` içine `packages` klasör.
    - Listelenen paketlerin geri `$(ProjectDir)\packages.config` içine `packages` klasör. Belirtilen her paket için paket paralel sürece geri yükleme `-DisableParallelProcessing` belirtilir.

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
