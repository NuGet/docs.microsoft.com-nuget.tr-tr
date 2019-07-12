---
title: Nuget.exe CLI kullanarak NuGet paketlerini Yönet
description: Nuget.exe CLI NuGet paketleri ile çalışmak için kullanma yönergeleri.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: a7177b956930835693921163e634321548c22462
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842364"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>Nuget.exe CLI kullanarak paketleri yönetme

CLI aracı kolayca güncelleştirmek ve projelerde ve çözümlerde NuGet paketlerini geri yüklemenize olanak sağlar. Bu araç tüm NuGet özellikleri Windows üzerinde sağlar ve ayrıca özelliklerinin çoğu Mac ve Linux üzerinde Mono altında çalışırken sağlar.

Nuget.exe CLI, .NET Framework projesi ve SDK stili projeleri (.NET Standard kitaplıkları hedefleyen Örneğin, bir SDK olmayan stil projeyi) içindir. İçin geçirilmiş olan bir SDK stili projesi kullanıyorsanız `PackageReference`, bunun yerine ' % s'dotnet CLI kullanın. NuGet CLI gerektiren bir [packages.config](../reference/packages-config.md) paket başvuruları için dosya.

> [!NOTE]
> Çoğu senaryoda öneririz [SDK stili projeleri geçirme](../reference/migrate-packages-config-to-package-reference.md) kullanan `packages.config` PackageReference için ve ardından dotnet CLI kullanabileceğiniz yerine `nuget.exe` CLI. Geçiş, C++ ve ASP.NET projeleri için şu anda kullanılabilir değil.

Bu makalede en yaygın nuget.exe CLI komutlarına birkaç temel kullanımını gösterir. Bir proje dosyası komutta belirtilmediği sürece bu komutların çoğu için CLI aracı bir proje dosyasını geçerli dizinde arar. Komut ve bağımsız değişkenler kullanabilirsiniz tam listesi için bkz: [nuget.exe CLI başvurusu](../tools/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Önkoşullar

- Yükleme `nuget.exe` ondan indirerek CLI [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), kaydetme `.exe` uygun bir klasöre dosya ve klasörün PATH ortam değişkeninize ekleme.

## <a name="install-a-package"></a>Paket yükleme

[Yükleme](../tools/cli-ref-install.md) komut indirir ve belirtilen paket kaynaklarını kullanan geçerli klasöre varsayarak, bir projeye bir paketi yükler. Yeni paketler halinde yükleme *paketleri* klasöründe proje kök dizini.

> [!IMPORTANT]
> `install`Komutu, bir proje dosyası değiştirmez veya *packages.config*; benzer şekilde, bu şekilde `restore` yalnızca diske paketleri ekler ancak bir proje bağımlılıklarınızı değiştirmez. Bir bağımlılık eklemek için Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi veya konsol üzerinden paket ekleme veya değiştirme *packages.config* ve ya da çalıştırın `install` veya `restore`.

1. Bir komut satırı açın ve proje dosyanızı içeren dizine geçin.

2. Bir NuGet paketini yüklemek için aşağıdaki komutu kullanın *paketleri* klasör.

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    Yüklenecek `Newtonsoft.json` paketini *paketleri* klasörüne aşağıdaki komutu kullanın:

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

Alternatif olarak, var olan bir bir NuGet paketini yüklemek için aşağıdaki komutu kullanabilirsiniz `packages.config` dosyasını *paketleri* klasör. Bu paket proje bağımlılıklarınızı eklemez, ancak yerel olarak yükler.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Bir paketi belirli bir sürümünü yükleme

Kullandığınız sürüm belirtilmezse [yükleme](../tools/cli-ref-install.md) komutu, NuGet paketinin en son sürümünü yükler. Bir Nuget paketi belirli bir sürümünü de yükleyebilirsiniz:

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Örneğin, 12.0.1 sürümünü eklemek için `Newtonsoft.json` paketi, bu komutu kullanın:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Sınırlamalar ve davranışı hakkında daha fazla bilgi için `install`, bkz: [paket yükleme](#install-a-package).

## <a name="remove-a-package"></a>Paket kaldırma

Bir veya daha fazla paket silmek için kaldırmak istediğiniz paketleri silmek *paketleri* klasör.

Paketleri yeniden yüklemek istiyorsanız, kullanın `restore` veya `install` komutu.

## <a name="list-packages"></a>Liste paketleri

Kullanarak belirtilen kaynak paketlerinin listesini görüntüleyebileceğiniz [listesi](../tools/cli-ref-list.md) komutu. Kullanım `-Source` arama kısıtlamak için seçeneği.

```cli
nuget list -Source <source>
```

Örneğin, paketleri listesi *paketleri* klasör.

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

Bir arama terimi kullanırsanız, arama, paketler, etiketler ve paket açıklamaları adlarını içerir.

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>Tek bir paket güncelleştirmesi

NuGet paketinin en son sürümünü yükler kullandığınızda `install` Paket sürümü belirtmediğiniz sürece komutu.

## <a name="update-all-packages"></a>Tüm paketleri güncelleştir

Kullanım [güncelleştirme](../tools/cli-ref-update.md) tüm paketleri Güncelleştir komutu. Güncelleştirmeleri bir projedeki tüm paketleri (kullanarak `packages.config`), en son kullanılabilir sürümler için. Çalıştırmak için önerilen `restore` çalıştırmadan önce `update`.

```cli
nuget update
```

## <a name="restore-packages"></a>Paketleri geri yükle

Kullanım [geri](../tools/cli-ref-restore.md) indirir ve yükler gelen eksik herhangi bir paket komutu *paketleri* klasör.

`restore` Yalnızca disk paketleri ekler, ancak bir proje bağımlılıklarınızı değiştirmez. Proje bağımlılıkları geri yüklemek için değiştirme `packages.config`, ardından `restore` komutu.

Olan diğer `dotnet` CLI komutları, ilk olarak bir komut satırı açın ve proje dosyanızı içeren dizine geçin.

Bir paketi kullanarak geri yüklemek için `restore`:

```cli
nuget restore MySolution.sln
```