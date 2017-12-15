---
title: NuGet CLI restore komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee41020-e548-4e61-b8cd-c82b77ac6af7
description: "Nuget.exe restore komutu için başvurusu"
keywords: "nuget başvuru geri yüklemek için restore paketleri komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b435a3c2ffe08e3c2f8fc6a4dacb06cf674e4fb9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="restore-command-nuget-cli"></a>Restore komutu (NuGet CLI)

**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** 2.7 +

NuGet 2.7 +: İndirir ve gelen eksik paketleri yükler `packages` klasör.

NuGet 3.3 + kullanarak projeleri ile `project.json`: oluşturan bir `project.lock.json` dosyası ve bir `<project>.nuget.props` gerekirse, dosya. (Her iki dosyası kaynak denetiminden atlanabilir.)

NuGet 4.0 + hangi başvuruları paketindeki proje dosyasında doğrudan projeyle: oluşturur bir `<project>.nuget.props` , gerekirse, dosya `obj` klasör. (Dosyası kaynak denetiminden atlanabilir.)

Mac OSX ve Linux Mono üzerinde CLI ile paketleri geri PackageReference biçimiyle desteklenmiyor.

## <a name="usage"></a>Kullanım

```
nuget restore <projectPath> [options]
```

Burada `<projectPath>` bir çözüm konumunu belirten bir `packages.config` dosya, veya bir `project.json` dosya. Bkz: [açıklamalar](#remarks) aşağıda davranış Ayrıntılar için.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır. |
| DirectDownload | *(4.0 +)*  Doğrudan önbellekleri herhangi bir ikili dosyaları veya meta veri ile doldurma olmadan paketleri yükler. |
| DisableParallelProcessing | Paralel olarak birden çok paket geri yükleme devre dışı bırakır. |
| FallbackSource | *(3.2 +)*  Paket birincil bulunamadığında durumunda geri dönüşler kullanmak için paket kaynaklarının listesi veya varsayılan kaynak. |
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| MSBuildPath | *(4.0 +)*  Öncelik Alma komutuyla kullanmak için MSBuild yolunu belirtir `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Bu komutla birlikte kullanılacak MSBuild sürümünü belirtir. Değerleri, 4, 12, 14, 15 desteklenir. MSBuild yolda çekilir varsayılan olarak, aksi takdirde MSBuild yüksek yüklü sürümü varsayar. |
| NoCache | NuGet paketleri yerel makine önbellekleri kullanmalarını engeller. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Çıktıdizini | Paketleri yüklendiği klasörü belirtir. Bir klasör bulunmadığından belirtilmezse, geçerli klasörde kullanılır. |
| PackageSaveMode | Paket yüklendikten sonra kaydetmek için dosya türlerini belirtir: biri `nuspec`, `nupkg`, veya `nuspec;nupkg`. |
| PackagesDirectory | Aynı `OutputDirectory`. |
| Project2ProjectTimeOut | Proje proje başvurularını çözümlemek için saniye cinsinden zaman aşımı. |
| Özyinelemeli | *(4.0 +)*  UWP ve .NET Core projeleri için tüm başvurular projeleri geri yükler. Kullanarak projeleri için geçerli değildir `packages.config`. |
| RequireConsent | Paketleri geri indirme ve yükleme paketleri önce etkin olduğunu doğrular. Ayrıntılar için bkz [paketi geri yüklemesi](../consume-packages/package-restore.md). |
| SolutionDirectory | Çözüm klasörü belirtir. Bir çözüm için paketleri geri yüklenirken geçerli değil. |
| Kaynak | Paket kaynaklarını listesini geri yüklemek için kullanılacak (URL'ler olarak) belirtir. Belirtilmezse, komut yapılandırma dosyalarında sağlanan kaynakları kullanır, bkz: [NuGet yapılandırma davranışı](../Consume-Packages/Configuring-NuGet-Behavior.md). |
| Ayrıntı Düzeyi |> çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *(2.5 +) ayrıntılı*. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="remarks"></a>Açıklamalar

Restore komutu aşağıdaki adımları gerçekleştirir:

1. Restore komutu, işlem modunu belirler.
    projectPath dosya türü | Davranış
    | --- | --- |
    Çözüm (klasör) | NuGet arar bir `.sln` dosya ve aksi takdirde bir hata verir kullanır. `(SolutionDir)\.nuget`Başlangıç klasörü olarak kullanılır.
    `.sln`Dosya | Çözümü tarafından tanımlanan paketler geri; bir hata durumunda verir `-SolutionDirectory` kullanılır. `$(SolutionDir)\.nuget`Başlangıç klasörü olarak kullanılır.
    `packages.config`, `project.json`, ya da proje dosyası | Çözümleme ve bağımlılıkları yükleme dosyasında listelenen paketler geri yükleyin.
    Başka bir dosya türü | Dosya olduğu varsayılır bir `.sln` dosya olarak yukarıdaki; yoksa bir çözüm, bir hata NuGet sağlar.
    (belirtilmezse projectPath) | -NuGet geçerli klasörde çözüm dosyalarını arar. Tek bir dosyada bulunursa, bir paketlerini geri yüklemek için kullanılır; birden çok çözüm bulunursa, NuGet hata verir.
    |-Hiçbir çözüm dosya varsa, NuGet arayan bir `packages.config` veya `project.json` ve bunu paketlerini geri yüklemek için kullanır.
    |-Çözüm dosyası yok varsa, `packages.config`, veya `project.json` bulunduğunda NuGet hata verir.

1. (Hiçbiri bu klasörlerin bulunmazsa NuGet hata verir) aşağıdaki öncelik sırasını kullanarak paketler klasörü belirleyin:

    - `%userprofile%\.nuget\packages` Değeri `project.json`.
    - İle belirtilen klasör `-PackagesDirectory`.
    - `repositoryPath` Hyperlink içinde`Nuget.Config`
    - İle belirtilen klasör`-SolutionDirectory`
    - `$(SolutionDir)\packages`

1. Bir çözüm için paketleri geri yüklenirken NuGet şunları yapar:
    - Çözüm dosyasını yükler.
    - Listelenen çözüm düzeyi paketlerini yükler `$(SolutionDir)\.nuget\packages.config` içine `packages` klasör.
    - Listelenen paketler geri `$(ProjectDir)\packages.config` içine `packages` klasör. Belirtilen her paket için paket paralel sürece geri `-DisableParallelProcessing` belirtilir.

## <a name="examples"></a>Örnekler

```
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
