---
title: "NuGet CLI yükleme komutunu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 59ac622f-837c-4545-bc93-a56330e02d71
description: "Nuget.exe yükleme komut başvurusu"
keywords: "nuget başvuru yükleyin, yükleme paketi komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88c123a7f2a3d628713cefcc4b110fb0205093b4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="install-command-nuget-cli"></a>Yükleme komutu (NuGet CLI)

**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** tüm

İndirir ve bir paket bir projeye geçerli klasörü belirtilen paket kaynaklarını kullanarak için varsayılan değer olarak yükler.

> [!Tip]
> Paket bir proje bağlamı dışında doğrudan indirmek için üzerinde paketin sayfasını ziyaret [nuget.org](https://www.nuget.org) seçip **karşıdan** bağlantı. 

Herhangi bir kaynağa belirtilirse, listelenenler genel yapılandırma dosyasında `%APPDATA%\NuGet\NuGet.Config`, kullanılır. Bkz: [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md) ek ayrıntılar için.

Özel paket belirtilirse, `install` projenin içinde listelenen tüm paketler yükler `packages.config` dosyasının benzer URL'ini [ `restore` ](#restore). ( `install` İle komutu çalışmıyor `project.json`.)

`install` Komutu bir proje dosyası değiştirilmez veya `packages.config`; bu şekilde, benzer `restore` yalnızca diske paketleri ekler ancak bir projenin bağımlılıkları değiştirmez.

Bir bağımlılık eklemek için Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi veya konsol üzerinden bir proje eklemek veya değiştirmek `packages.config` ve ardından çalıştırın `install` veya `restore`. Kullanarak projeleri için `project.json`, bu dosyayı değiştirmek ve ardından çalıştırın `restore`.

## <a name="usage"></a>Kullanım

```
nuget install <packageID | configFilePath> [options]
```

Burada `<packageID>` (en son sürümünü kullanarak), yüklenecek paketin adları veya `<configFilePath>` tanımlayan `packages.config` yüklenecek paketleri listeleyen dosya. Belirli bir sürümle belirtebilir `-Version` seçeneği.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | *(2.5 +)*  Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır. |
| DisableParallelProcessing | Paralel olarak birden çok paket yüklemeyi devre dışı bırakır. |
| ExcludeVersion | Yalnızca paket adı ve sürüm numarası ile adlı bir klasöre paketi yükler. |
| FallbackSource | *(3.2 +)*  Paket birincil bulunamadığında durumunda geri dönüşler kullanmak için paket kaynaklarının listesi veya varsayılan kaynak. |
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Framework | *(4.4 +)*  Hedef framework bağımlılıkları seçmek için kullanılır. Varsayılan olarak 'Any' belirtilmediği takdirde. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| NoCache | NuGet paketleri yerel makine önbellekleri kullanmalarını engeller. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Çıktıdizini | Paketleri yüklendiği klasörü belirtir. Bir klasör bulunmadığından belirtilmezse, geçerli klasörde kullanılır. |
| PackageSaveMode | Paket yüklendikten sonra kaydetmek için dosya türlerini belirtir: biri `nuspec`, `nupkg`, veya `nuspec;nupkg`. |
| Yayın öncesi | Yayın öncesi paketlerin yüklenmesini sağlar. Bu bayrak paketleri geri yüklenirken gerekli değil `packages.config`. |
| RequireConsent | Paketleri geri indirme ve yükleme paketleri önce etkin olduğunu doğrular. Ayrıntılar için bkz [paketi geri yüklemesi](../consume-packages/package-restore.md). |
| SolutionDirectory | Paketler geri yükleneceği için çözümün kök klasörü belirtir. |
| Kaynak | Paket kaynaklarını listesini kullanmak için (URL) belirtir. Belirtilmezse, komut yapılandırma dosyalarında sağlanan kaynakları kullanır, bkz: [NuGet yapılandırma davranışı](../Consume-Packages/Configuring-NuGet-Behavior.md). |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *(2.5 +) ayrıntılı*. |
| Sürüm | Yüklenecek paketin sürümünü belirtir. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
