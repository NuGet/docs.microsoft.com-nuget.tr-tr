---
title: NuGet CLI yükleme komutu
description: Nuget.exe yüklemesi komut başvurusu
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 8261cdb83af72d9d9379124f4c446c7cd2a50299
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549142"
---
# <a name="install-command-nuget-cli"></a>Yükleme komutu (NuGet CLI)

**İçin geçerlidir:** paketini tüketim &bullet; **desteklenen sürümler:** tüm

İndirir ve belirtilen paket kaynaklarını kullanan geçerli klasöre varsayarak, bir projeye bir paketi yükler.

> [!Tip]
> Doğrudan projenin bağlamı dışında bir paketini indirmek için paketin sayfasını ziyaret edin [nuget.org](https://www.nuget.org) seçip **indirme** bağlantı.

Bu kaynağı yok belirtilirse, genel yapılandırma dosyasında listelenen `%appdata%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır. Bkz: [yapılandırma NuGet davranışını](../consume-packages/configuring-nuget-behavior.md) bakın.

Belirli bir paket yok belirtilirse, `install` projenin içinde listelenen tüm paketleri yükler `packages.config` dosyasının benzer URL'ini [ `restore` ](cli-ref-restore.md).

`install` Komutu, bir proje dosyası değiştirmez veya `packages.config`; benzer şekilde, bu şekilde `restore` yalnızca diske paketleri ekler ancak bir proje bağımlılıklarınızı değiştirmez.

Bir bağımlılık eklemek için Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi veya konsol üzerinden paket ekleme veya değiştirme `packages.config` ve ya da çalıştırın `install` veya `restore`.

## <a name="usage"></a>Kullanım

```cli
nuget install <packageID | configFilePath> [options]
```

Burada `<packageID>` (en son sürümünü kullanarak), yüklemek için paketi adları veya `<configFilePath>` tanımlayan `packages.config` paketlerin yüklenmesi listeleyen dosyası. Belirli bir sürümle belirtebilir `-Version` seçeneği.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| DependencyVersion | *(4.4 +)*  , Aşağıdakilerden herhangi birini kullanmak için bağımlılık paketlerini sürümü:<br/><ul><li>*En düşük* (varsayılan): en düşük sürüm</li><li>*HighestPatch*: en düşük büyük, en düşük küçük, yüksek düzeltme sürümü</li><li>*HighestMinor*: en düşük ana sürümle, en yüksek ikincil, yüksek düzeltme eki</li><li>*En yüksek*: en yüksek sürüm</li></ul> |
| DisableParallelProcessing | Paralel olarak birden fazla paket yükleme devre dışı bırakır. |
| ExcludeVersion | Paketin, paket adı ve sürüm numarası ile adlı bir klasöre yükler. |
| FallbackSource | *(3.2 +)*  Paketi birincil bulunamadığında durumunda geri dönüşler kullanmak için paket kaynaklarının bir listesini ya da varsayılan kaynak. |
| ForceEnglishOutput | *(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar. |
| Framework | *(4.4 +)*  Hedef Framework'ü bağımlılıkları seçmek amacıyla kullanılır. Varsayılan olarak 'Any' belirtilmediği takdirde. |
| Yardım | Bilgi komut için yardımı görüntüler. |
| NoCache | NuGet, önbelleğe eklenen paketler kullanmasını önler. Bkz: [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Kullanıcı girişini veya onaylar ister bastırır. |
| OutputDirectory | Paket yüklendiği klasörünü belirtir. Klasör belirtilirse, geçerli klasörde kullanılır. |
| PackageSaveMode | Paket yükleme sonrasında kaydedilecek dosya türlerini belirtir: biri `nuspec`, `nupkg`, veya `nuspec;nupkg`. |
| Yayın öncesi | Yayın öncesi paketleri yüklü olmasını sağlar. Bu bayrak paketlerle geri yüklerken gerekli değil `packages.config`. |
| RequireConsent | Paketleri geri yükleme ve paketleri yüklemeden önce etkin olduğunu doğrular. Ayrıntılar için bkz [paketi geri yüklemeyi](../consume-packages/package-restore.md). |
| SolutionDirectory | Çözüm için paketler geri yükleneceği kök klasörünü belirtir. |
| Kaynak | Paket kaynaklarının listesi (URL'ler) kullanılması gerektiğini belirtir. Atlanırsa, komut yapılandırma dosyalarında sağlanan kaynakları kullanır, bkz: [yapılandırma NuGet davranışını](../consume-packages/configuring-nuget-behavior.md). |
| Ayrıntı Düzeyi | Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |
| Sürüm | Yüklemek için paketi sürümünü belirtir. |

Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
