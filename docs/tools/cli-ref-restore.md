---
title: NuGet CLI restore komutu
description: Nuget.exe restore komutu için başvurusu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4df7685883fea78428c6744bdbf4c66d83e469bc
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817924"
---
# <a name="restore-command-nuget-cli"></a>Restore komutu (NuGet CLI)

**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** 2.7 +

İndirir ve gelen eksik paketleri yükler `packages` klasör. NuGet 4.0 + ve PackageReference biçimi ile kullanıldığında, oluşturan bir `<project>.nuget.props` , gerekirse, dosya `obj` klasör. (Dosyası kaynak denetiminden atlanabilir.)

Mac OSX ve Linux Mono üzerinde CLI ile paketleri geri PackageReference ile desteklenmiyor.

## <a name="usage"></a>Kullanım

```cli
nuget restore <projectPath> [options]
```

Burada `<projectPath>` bir çözüm konumunu belirtir veya `packages.config` dosyası. Bkz: [açıklamalar](#remarks) aşağıda davranış Ayrıntılar için.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| DirectDownload | *(4.0 +)*  Doğrudan önbellekleri herhangi bir ikili dosyaları veya meta veri ile doldurma olmadan paketleri yükler. |
| DisableParallelProcessing | Paralel olarak birden çok paket geri yükleme devre dışı bırakır. |
| FallbackSource | *(3.2 +)*  Paket birincil bulunamadığında durumunda geri dönüşler kullanmak için paket kaynaklarının listesi veya varsayılan kaynak. |
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| MSBuildPath | *(4.0 +)*  Öncelik Alma komutuyla kullanmak için MSBuild yolunu belirtir `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Bu komutla birlikte kullanılacak MSBuild sürümünü belirtir. Değerleri, 4, 12, 14, 15 desteklenir. MSBuild yolda çekilir varsayılan olarak, aksi takdirde MSBuild yüksek yüklü sürümü varsayar. |
| NoCache | NuGet kullanarak önbelleğe alınmış paketleri engeller. Bkz: [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Kullanıcı girişi veya onayı için ister gizler. |
| OutputDirectory | Paketleri yüklendiği klasörü belirtir. Bir klasör bulunmadığından belirtilmezse, geçerli klasörde kullanılır. İle geri yüklerken gerekli bir `packages.config` sürece dosya `PackagesDirectory` veya `SolutionDirectory` kullanılır.|
| PackageSaveMode | Paket yüklendikten sonra kaydetmek için dosya türlerini belirtir: biri `nuspec`, `nupkg`, veya `nuspec;nupkg`. |
| PackagesDirectory | Aynı `OutputDirectory`. İle geri yüklerken gerekli bir `packages.config` sürece dosya `OutputDirectory` veya `SolutionDirectory` kullanılır. |
| Project2ProjectTimeOut | Proje proje başvurularını çözümlemek için saniye cinsinden zaman aşımı. |
| Özyinelemeli | *(4.0 +)*  UWP ve .NET Core projeleri için tüm başvurular projeleri geri yükler. Kullanarak projeleri için geçerli değildir `packages.config`. |
| RequireConsent | Paketleri geri indirme ve yükleme paketleri önce etkin olduğunu doğrular. Ayrıntılar için bkz [paketi geri yüklemesi](../consume-packages/package-restore.md). |
| SolutionDirectory | Çözüm klasörü belirtir. Bir çözüm için paketleri geri yüklenirken geçerli değil. İle geri yüklerken gerekli bir `packages.config` sürece dosya `PackagesDirectory` veya `OutputDirectory` kullanılır. |
| Kaynak | Paket kaynaklarını listesini geri yüklemek için kullanılacak (URL'ler olarak) belirtir. Belirtilmezse, komut yapılandırma dosyalarında sağlanan kaynakları kullanır, bkz: [NuGet yapılandırma davranışı](../consume-packages/configuring-nuget-behavior.md). |
| Ayrıntı Düzeyi |> çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="remarks"></a>Açıklamalar

Restore komutu aşağıdaki adımları gerçekleştirir:

1. Restore komutu, işlem modunu belirler.

   | projectPath dosya türü | Davranış |
   | --- | --- |
   | Çözüm (klasör) | NuGet arar bir `.sln` dosya ve aksi takdirde bir hata verir kullanır. `(SolutionDir)\.nuget` Başlangıç klasörü olarak kullanılır. |
   | `.sln` Dosya | Çözümü tarafından tanımlanan paketler geri; bir hata durumunda verir `-SolutionDirectory` kullanılır. `$(SolutionDir)\.nuget` Başlangıç klasörü olarak kullanılır. |
   | `packages.config` ya da proje dosyası | Çözümleme ve bağımlılıkları yükleme dosyasında listelenen paketler geri yükleyin. |
   | Başka bir dosya türü | Dosya olduğu varsayılır bir `.sln` dosya olarak yukarıdaki; yoksa bir çözüm, bir hata NuGet sağlar. |
   | (belirtilmezse projectPath) | <ul><li>NuGet geçerli klasörde çözüm dosyalarını arar. Tek bir dosyada bulunursa, bir paketlerini geri yüklemek için kullanılır; birden çok çözüm bulunursa, NuGet hata verir.</li><li>Çözüm dosya yoksa NuGet arayan bir `packages.config` ve bunu paketlerini geri yüklemek için kullanır.</li><li>Çözüm varsa veya `packages.config` dosya bulunduğunda, NuGet hata verir.</ul> |

2. (Hiçbiri bu klasörlerin bulunmazsa NuGet hata verir) aşağıdaki öncelik sırasını kullanarak paketler klasörü belirleyin:

    - İle belirtilen klasör `-PackagesDirectory`.
    - `repositoryPath` Hyperlink içinde `Nuget.Config`
    - İle belirtilen klasör `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Bir çözüm için paketleri geri yüklenirken NuGet şunları yapar:
    - Çözüm dosyasını yükler.
    - Listelenen çözüm düzeyi paketlerini yükler `$(SolutionDir)\.nuget\packages.config` içine `packages` klasör.
    - Listelenen paketler geri `$(ProjectDir)\packages.config` içine `packages` klasör. Belirtilen her paket için paket paralel sürece geri `-DisableParallelProcessing` belirtilir.

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
