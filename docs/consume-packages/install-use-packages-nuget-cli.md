---
title: NuGet. exe CLı kullanarak NuGet paketlerini yönetme
description: NuGet paketleri ile çalışmak için NuGet. exe CLı kullanma yönergeleri.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 9eefed6f2c1a362f27c4a5d33d07645d743379fa
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317741"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>NuGet. exe CLı kullanarak paketleri yönetme

CLı Aracı, projelerde ve çözümlerinde NuGet paketlerini kolayca güncelleştirmenize ve geri yüklemenize olanak tanır. Bu araç Windows üzerinde tüm NuGet yeteneklerini sağlar ve ayrıca Mono altında çalışırken Mac ve Linux özelliklerinin çoğunu sağlar.

`nuget.exe` CLI .NET Framework projeniz ve SDK olmayan bir stil projem (örneğin, .NET Standard kitaplıklarını hedefleyen SDK olmayan bir stil Projesi) içindir. Öğesine `PackageReference`geçirilmiş SDK olmayan bir proje kullanıyorsanız bunun yerine `dotnet` CLI kullanın. CLI `nuget.exe` , paket başvuruları için bir [Packages. config](../reference/packages-config.md) dosyası gerektirir.

> [!NOTE]
> Çoğu senaryoda, packagereference için kullanılan `packages.config` [SDK olmayan projeler arasında geçiş](../reference/migrate-packages-config-to-package-reference.md) `dotnet` yapmanızı öneririz ve `nuget.exe` CLI yerine CLI kullanabilirsiniz. Geçiş Şu anda ve ASP.NET projeleri C++ için kullanılabilir değil.

Bu makalede, en sık kullanılan `nuget.exe` CLI komutlarının birçoğuna ilişkin temel kullanım gösterilmektedir. Bu komutların çoğu için, komutta bir proje dosyası belirtilmediği takdirde CLı aracı geçerli dizinde bir proje dosyası arar. Komutların ve kullanabileceğiniz bağımsız değişkenlerin tamamı listesi için bkz. [NuGet. exe CLI başvurusu](../reference/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Önkoşullar

- [NuGet.org adresinden](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)indirerek, bu `.exe` dosyayı uygun bir klasöre kaydederek ve bu klasörü PATH ortam değişkeninizden ekleyerek CLI'yıyükleme.`nuget.exe`

## <a name="install-a-package"></a>Paket yükler

[Install](../reference/cli-reference/cli-ref-install.md) komutu, belirtilen paket kaynaklarını kullanarak bir paketi indirir ve geçerli klasörü varsayılan olarak bir projeye yükler. Yeni paketleri proje kök dizininizde *paketler* klasörüne yükler.

> [!IMPORTANT]
> Komut bir proje dosyasını veya *Packages. config*; bu şekilde, yalnızca paketleri diske eklemesine, ancak projenin bağımlılıklarını `restore` değiştirmediğinden bu şekilde değişiklik yapmaz. `install` Bir bağımlılık eklemek için, Visual Studio 'da Paket Yöneticisi Kullanıcı arabirimi veya konsolundan bir paket ekleyin veya *Packages. config dosyasını* değiştirip ya `install` `restore`da çalıştırın.

1. Bir komut satırı açın ve proje dosyanızı içeren dizine geçiş yapın.

2. *Packages* klasörüne bir NuGet paketi yüklemek için aşağıdaki komutu kullanın.

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    `Newtonsoft.json` Paketi *paketler* klasörüne yüklemek için şu komutu kullanın:

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

Alternatif olarak, `packages.config` *paketler* klasörüne var olan bir dosyayı kullanarak bir NuGet paketini yüklemek için aşağıdaki komutu kullanabilirsiniz. Bu, paketi proje bağımlılıklarınızla eklemez, ancak yerel olarak yüklemez.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Bir paketin belirli bir sürümünü yükler

[Yükleme](../reference/cli-reference/cli-ref-install.md) komutunu kullandığınızda sürüm belirtilmemişse, NuGet paketin en son sürümünü yükler. Ayrıca, bir NuGet paketinin belirli bir sürümünü de yükleyebilirsiniz:

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Örneğin, `Newtonsoft.json` paketin sürüm 12.0.1 ' i eklemek için şu komutu kullanın:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Sınırlamaları ve davranışı `install`hakkında daha fazla bilgi için bkz. [paket yüklemesi](#install-a-package).

## <a name="remove-a-package"></a>Bir paketi kaldırma

Bir veya daha fazla paketi silmek için, *paketler* klasöründen kaldırmak istediğiniz paketleri silin.

Paketleri yeniden yüklemek istiyorsanız `restore` veya `install` komutunu kullanın.

## <a name="list-packages"></a>Paketleri Listele

[Liste](../reference/cli-reference/cli-ref-list.md) komutunu kullanarak belirli bir kaynaktaki paketlerin listesini görüntüleyebilirsiniz. Aramayı kısıtlamak için seçeneğini kullanın. `-Source`

```cli
nuget list -Source <source>
```

Örneğin, *paketler klasöründeki paketleri* listeleyin.

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

Arama terimi kullanırsanız, arama paket, etiket ve paket açıklamalarının adlarını içerir.

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>Tek bir paketi güncelleştirme

Paket sürümünü belirtmediğiniz takdirde NuGet, `install` komutunu kullandığınızda paketin en son sürümünü yüklenir.

## <a name="update-all-packages"></a>Tüm paketleri Güncelleştir

Tüm paketleri güncelleştirmek için [Güncelleştir](../reference/cli-reference/cli-ref-update.md) komutunu kullanın. Projedeki tüm paketleri (kullanarak `packages.config`) en son kullanılabilir sürümlerine güncelleştirir. `restore` Çalıştırılmadan`update`önce çalıştırılması önerilir.

```cli
nuget update
```

## <a name="restore-packages"></a>Paketleri geri yükle

*Paketler* klasöründe eksik olan paketleri indiren ve yükleyen [restore](../reference/cli-reference/cli-ref-restore.md) komutunu kullanın.

`restore`yalnızca paketleri diske ekler ancak projenin bağımlılıklarını değiştirmez. Proje bağımlılıklarını geri yüklemek için, `packages.config`öğesini değiştirin, sonra `restore` komutunu kullanın.

Diğer `nuget.exe` CLI komutlarında olduğu gibi, önce bir komut satırını açın ve proje dosyanızı içeren dizine geçiş yapın.

Paketini kullanarak `restore`geri yüklemek için:

```cli
nuget restore MySolution.sln
```