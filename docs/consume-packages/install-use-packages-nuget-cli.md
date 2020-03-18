---
title: NuGet. exe CLı kullanarak NuGet paketlerini yönetme
description: NuGet paketleri ile çalışmak için NuGet. exe CLı kullanma yönergeleri.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428690"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>NuGet. exe CLı kullanarak paketleri yönetme

CLı Aracı, projelerde ve çözümlerinde NuGet paketlerini kolayca güncelleştirmenize ve geri yüklemenize olanak tanır. Bu araç Windows üzerinde tüm NuGet yeteneklerini sağlar ve ayrıca Mono altında çalışırken Mac ve Linux özelliklerinin çoğunu sağlar.

`nuget.exe` CLı, .NET Framework projeniz ve SDK olmayan bir stil projesi (örneğin, .NET Standard kitaplıklarını hedefleyen SDK olmayan bir stil Projesi) içindir. `PackageReference`'e geçirilmiş SDK olmayan bir proje kullanıyorsanız bunun yerine `dotnet` CLı kullanın. `nuget.exe` CLı, paket başvuruları için bir [Packages. config](../reference/packages-config.md) dosyası gerektirir.

> [!NOTE]
> Çoğu senaryoda, `packages.config` kullanan [SDK olmayan projelerin](../consume-packages/migrate-packages-config-to-package-reference.md) packagereference 'a geçirilmesini öneririz ve sonra `nuget.exe` clı yerıne `dotnet` CLI kullanabilirsiniz. Geçiş Şu anda ve ASP.NET projeleri C++ için kullanılabilir değil.

Bu makale, en sık kullanılan `nuget.exe` CLı komutlarının bir bölümünü temel olarak gösterir. Bu komutların çoğu için, komutta bir proje dosyası belirtilmediği takdirde CLı aracı geçerli dizinde bir proje dosyası arar. Komutların ve kullanabileceğiniz bağımsız değişkenlerin tamamı listesi için bkz. [NuGet. exe CLI başvurusu](../reference/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Önkoşullar

- [NuGet.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)adresinden INDIREREK `nuget.exe` CLI yükleme, bu `.exe` dosyayı uygun bir klasöre kaydetme ve bu klasörü PATH ortam değişkeninizden ekleme.

## <a name="install-a-package"></a>Paket yükler

[Install](../reference/cli-reference/cli-ref-install.md) komutu, belirtilen paket kaynaklarını kullanarak bir paketi indirir ve geçerli klasörü varsayılan olarak bir projeye yükler. Yeni paketleri proje kök dizininizde *paketler* klasörüne yükler.

> [!IMPORTANT]
> `install`komutu bir proje dosyası veya *Packages. config*dosyasını değiştirmez; Bu şekilde, yalnızca paketleri diske eklemesi, ancak projenin bağımlılıklarını değiştirmediğinden `restore` benzerdir. Bir bağımlılık eklemek için, Visual Studio 'da Paket Yöneticisi Kullanıcı arabirimi veya konsolundan bir paket ekleyin veya *Packages. config dosyasını* değiştirip `install` ya da `restore`çalıştırın.

1. Bir komut satırı açın ve proje dosyanızı içeren dizine geçiş yapın.

2. *Packages* klasörüne bir NuGet paketi yüklemek için aşağıdaki komutu kullanın.

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    *Paketler* klasörüne `Newtonsoft.json` paketini yüklemek için aşağıdaki komutu kullanın:

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

Alternatif olarak, *paketler* klasörüne mevcut bir `packages.config` dosyasını kullanarak bir NuGet paketini yüklemek için aşağıdaki komutu kullanabilirsiniz. Bu, paketi proje bağımlılıklarınızla eklemez, ancak yerel olarak yüklemez.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Bir paketin belirli bir sürümünü yükler

[Yükleme](../reference/cli-reference/cli-ref-install.md) komutunu kullandığınızda sürüm belirtilmemişse, NuGet paketin en son sürümünü yükler. Ayrıca, bir NuGet paketinin belirli bir sürümünü de yükleyebilirsiniz:

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Örneğin, `Newtonsoft.json` paketinin 12.0.1 sürümünü eklemek için şu komutu kullanın:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

`install`kısıtlamaları ve davranışı hakkında daha fazla bilgi için bkz. [paket yüklemesi](#install-a-package).

## <a name="remove-a-package"></a>Bir paketi kaldırma

Bir veya daha fazla paketi silmek için, *paketler* klasöründen kaldırmak istediğiniz paketleri silin.

Paketleri yeniden yüklemek istiyorsanız `restore` veya `install` komutunu kullanın.

## <a name="list-packages"></a>Paketleri Listele

[Liste](../reference/cli-reference/cli-ref-list.md) komutunu kullanarak belirli bir kaynaktaki paketlerin listesini görüntüleyebilirsiniz. Aramayı kısıtlamak için `-Source` seçeneğini kullanın.

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

Paket sürümünü belirtmediğiniz takdirde NuGet, `install` komutunu kullandığınızda paketin en son sürümünü yüklenir.

## <a name="update-all-packages"></a>Tüm paketleri Güncelleştir

Tüm paketleri güncelleştirmek için [Güncelleştir](../reference/cli-reference/cli-ref-update.md) komutunu kullanın. Projedeki tüm paketleri (`packages.config`kullanarak) en son kullanılabilir sürümlerine güncelleştirir. `update`çalıştırılmadan önce `restore` çalıştırılması önerilir.

```cli
nuget update
```

## <a name="restore-packages"></a>Paketleri geri yükle

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a>CLı sürümünü al

Şu komutu kullanın:

```cli
nuget help
```

Yardım çıkışının ilk satırı sürümü gösterir. Yukarı kaydırmaktan kaçınmak için, bunun yerine `nuget help | more` kullanın.