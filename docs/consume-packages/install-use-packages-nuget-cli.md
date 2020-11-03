---
title: nuget.exe CLı kullanarak NuGet paketlerini yönetme
description: NuGet paketleriyle çalışmak için nuget.exe CLı kullanma yönergeleri.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237393"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>nuget.exe CLı kullanarak paketleri yönetme

CLı Aracı, projelerde ve çözümlerinde NuGet paketlerini kolayca güncelleştirmenize ve geri yüklemenize olanak tanır. Bu araç Windows üzerinde tüm NuGet yeteneklerini sağlar ve ayrıca Mono altında çalışırken Mac ve Linux özelliklerinin çoğunu sağlar.

`nuget.exe`Clı .NET Framework projeniz ve SDK olmayan bir stil projem (örneğin, .NET Standard kitaplıklarını hedefleyen SDK olmayan bir stil Projesi) içindir. Öğesine geçirilmiş SDK olmayan bir proje kullanıyorsanız `PackageReference` `dotnet` bunun yerine CLI kullanın. `nuget.exe`CLI, paket başvuruları için bir [packages.config](../reference/packages-config.md) dosyası gerektirir.

> [!NOTE]
> Çoğu senaryoda, PackageReference için kullanılan [SDK olmayan projeler arasında geçiş](../consume-packages/migrate-packages-config-to-package-reference.md) `packages.config` yapmanızı öneririz ve `dotnet` CLI yerine CLI kullanabilirsiniz `nuget.exe` . Geçiş Şu anda C++ ve ASP.NET projeleri için kullanılabilir değil.

Bu makalede, en sık kullanılan CLI komutlarının birçoğuna ilişkin temel kullanım gösterilmektedir `nuget.exe` . Bu komutların çoğu için, komutta bir proje dosyası belirtilmediği takdirde CLı aracı geçerli dizinde bir proje dosyası arar. Komutların ve kullanabileceğiniz bağımsız değişkenlerin tamamı listesi için [nuget.exe CLI başvurusuna](../reference/nuget-exe-cli-reference.md)bakın.

## <a name="prerequisites"></a>Önkoşullar

- `nuget.exe` [NuGet.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)adresinden indirerek, bu `.exe` dosyayı uygun bir klasöre KAYDEDEREK ve bu klasörü PATH ortam değişkeninizden ekleyerek CLI 'yı yükleme.

## <a name="install-a-package"></a>Paketi yükleme

[Install](../reference/cli-reference/cli-ref-install.md) komutu, belirtilen paket kaynaklarını kullanarak bir paketi indirir ve geçerli klasörü varsayılan olarak bir projeye yükler. Yeni paketleri proje kök dizininizde *paketler* klasörüne yükler.

> [!IMPORTANT]
> `install`Komut bir proje dosyasını veya *packages.config* değiştirmez; buna benzer şekilde, `restore` yalnızca paketleri diske eklemektedir ancak projenin bağımlılıklarını değiştirmez. Bir bağımlılık eklemek için, Visual Studio 'da Paket Yöneticisi Kullanıcı arabirimi veya konsolundan bir paket ekleyin veya *packages.config* değiştirin ve sonra ya da çalıştırın `install` `restore` .

1. Bir komut satırı açın ve proje dosyanızı içeren dizine geçiş yapın.

2. *Packages* klasörüne bir NuGet paketi yüklemek için aşağıdaki komutu kullanın.

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    `Newtonsoft.json`Paketi *paketler* klasörüne yüklemek için şu komutu kullanın:

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

Alternatif olarak, paketler klasörüne var olan bir dosyayı kullanarak bir NuGet paketini yüklemek için aşağıdaki komutu kullanabilirsiniz `packages.config` . *packages* Bu, paketi proje bağımlılıklarınızla eklemez, ancak yerel olarak yüklemez.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Bir paketin belirli bir sürümünü yükler

[Yükleme](../reference/cli-reference/cli-ref-install.md) komutunu kullandığınızda sürüm belirtilmemişse, NuGet paketin en son sürümünü yükler. Ayrıca, bir NuGet paketinin belirli bir sürümünü de yükleyebilirsiniz:

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Örneğin, paketin sürüm 12.0.1 ' i eklemek için `Newtonsoft.json` Şu komutu kullanın:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Sınırlamaları ve davranışı hakkında daha fazla bilgi için `install` bkz. [paket yüklemesi](#install-a-package).

## <a name="remove-a-package"></a>Bir paketi kaldırma

Bir veya daha fazla paketi silmek için, *paketler* klasöründen kaldırmak istediğiniz paketleri silin.

Paketleri yeniden yüklemek istiyorsanız `restore` veya `install` komutunu kullanın.

## <a name="list-packages"></a>Paketleri Listele

[Liste](../reference/cli-reference/cli-ref-list.md) komutunu kullanarak belirli bir kaynaktaki paketlerin listesini görüntüleyebilirsiniz. `-Source`Aramayı kısıtlamak için seçeneğini kullanın.

```cli
nuget list -Source <source>
```

Örneğin *, paketler klasöründeki paketleri* listeleyin.

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

Arama terimi kullanırsanız, arama paket, etiket ve paket açıklamalarının adlarını içerir.

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>Tek bir paketi güncelleştirme

Paket sürümünü belirtmediğiniz takdirde NuGet, komutunu kullandığınızda paketin en son sürümünü yüklenir `install` .

## <a name="update-all-packages"></a>Tüm paketleri Güncelleştir

Tüm paketleri güncelleştirmek için [Güncelleştir](../reference/cli-reference/cli-ref-update.md) komutunu kullanın. Projedeki tüm paketleri (kullanarak `packages.config` ) en son kullanılabilir sürümlerine güncelleştirir. Çalıştırılmadan önce çalıştırılması önerilir `restore` `update` .

```cli
nuget update
```

## <a name="restore-packages"></a>Paketleri geri yükleme

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a>CLı sürümünü al

Şu komutu çalıştırın:

```cli
nuget help
```

Yardım çıkışının ilk satırı sürümü gösterir. Yukarı kaydırmayı önlemek için `nuget help | more` bunun yerine kullanın.