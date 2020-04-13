---
title: Nuget.exe CLI'yi kullanarak NuGet paketlerini yönetin
description: NuGet paketleri ile çalışmak için nuget.exe CLI kullanma talimatları.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428690"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>nuget.exe CLI kullanarak paketleri yönetme

CLI aracı, projelerde ve çözümlerde NuGet paketlerini kolayca güncellemenize ve geri yüklemenize olanak tanır. Bu araç, Windows'daki tüm NuGet özelliklerini sağlar ve Mono altında çalışırken Mac ve Linux'taki birçok özelliği de sağlar.

`nuget.exe` CLI, .NET Framework projeniz ve SDK tarzı olmayan projeleriniz içindir (örneğin, .NET Standart kitaplıklarını hedefleyen SDK tarzı olmayan bir proje). Geçiş yapılan SDK tarzı olmayan bir proje `PackageReference`kullanıyorsanız, bunun `dotnet` yerine CLI'yi kullanın. `nuget.exe` CLI, paket başvuruları için bir [packages.config](../reference/packages-config.md) dosyası gerektirir.

> [!NOTE]
> Çoğu senaryoda, PackageReference için kullanılan `packages.config` [SDK tarzı olmayan projeleri geçirmenizi](../consume-packages/migrate-packages-config-to-package-reference.md) öneririz `dotnet` ve ardından `nuget.exe` CLI yerine CLI'yi kullanabilirsiniz. Geçiş şu anda C++ ve ASP.NET projeleri için kullanılamıyor.

Bu makalede, en yaygın `nuget.exe` CLI komutlarından birkaçı için temel kullanım gösterilmektedir. Bu komutların çoğu nda, komutta bir proje dosyası belirtilmediği sürece CLI aracı geçerli dizinde bir proje dosyası arar. Komutların ve kullanabileceğiniz bağımsız değişkenlerin tam listesi için [nuget.exe CLI başvurusuna](../reference/nuget-exe-cli-reference.md)bakın.

## <a name="prerequisites"></a>Ön koşullar

- CLI'yi `nuget.exe` [nuget.org'dan](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)indirerek yükleyin, dosyayı `.exe` uygun bir klasöre kaydedin ve bu klasörü PATH ortamı değişkeninize eklediniz.

## <a name="install-a-package"></a>Paket yükleme

[Install](../reference/cli-reference/cli-ref-install.md) komutu, belirtilen paket kaynaklarını kullanarak geçerli klasöre varsayılan olarak bir paketi indirir ve projeye yükler. Proje kök dizininizdeki *paketler* klasörüne yeni paketler yükleyin.

> [!IMPORTANT]
> Komut, `install`proje dosyasını veya *packages.config'i*değiştirmez; bu şekilde, `restore` yalnızca diske paket eklediği, ancak projenin bağımlılıklarını değiştirmemesi benzer. Bağımlılık eklemek için Visual Studio'daki Paket Yöneticisi UI veya Console üzerinden paket ekleyin veya *packages.config'i* değiştirin ve sonra ya da `install` `restore`çalıştırın.

1. Bir komut satırı açın ve proje dosyanızı içeren dizine geçin.

2. *Paketler* klasörüne bir NuGet paketi yüklemek için aşağıdaki komutu kullanın.

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    Paketi `Newtonsoft.json` *paketler* klasörüne yüklemek için aşağıdaki komutu kullanın:

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

Alternatif olarak, `packages.config` *paketler* klasörüne varolan bir dosyayı kullanarak bir NuGet paketi yüklemek için aşağıdaki komutu kullanabilirsiniz. Bu, paketi proje bağımlılıklarınıza eklemez, ancak yerel olarak yükler.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Paketin belirli bir sürümünü yükleme

[Yükleme](../reference/cli-reference/cli-ref-install.md) komutunu kullandığınızda sürüm belirtilmemişse, NuGet paketin en son sürümünü yükler. Nuget paketinin belirli bir sürümünü de yükleyebilirsiniz:

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Örneğin, `Newtonsoft.json` paketin 12.0.1 sürümünü eklemek için şu komutu kullanın:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Sınırlamalar ve davranışlar hakkında `install`daha fazla bilgi için [bkz.](#install-a-package)

## <a name="remove-a-package"></a>Paketi kaldırma

Bir veya daha fazla paketi silmek *için, paketler* klasöründen kaldırmak istediğiniz paketleri silin.

Paketleri yeniden yüklemek istiyorsanız, `restore` komutu `install` kullanın.

## <a name="list-packages"></a>Paketleri listele

[Liste](../reference/cli-reference/cli-ref-list.md) komutunu kullanarak belirli bir kaynaktan gelen paketlerin listesini görüntüleyebilirsiniz. Aramayı `-Source` kısıtlama seçeneğini kullanın.

```cli
nuget list -Source <source>
```

Örneğin, *paketleri paketler* klasörüne listeleyin.

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

Arama terimi kullanıyorsanız, arama paketlerin, etiketlerin ve paket açıklamalarının adlarını içerir.

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>Tek bir paketi güncelleştirme

NuGet, paket sürümünü belirtmediğiniz sürece `install` komutu kullandığınızda paketin en son sürümünü yükler.

## <a name="update-all-packages"></a>Tüm paketleri güncelleştirin

Tüm paketleri güncelleştirmek için [güncelleştirme](../reference/cli-reference/cli-ref-update.md) komutunu kullanın. Projedeki (kullanarak) `packages.config`tüm paketleri en son kullanılabilir sürümleriyle güncelleştirir. Çalıştırmadan önce `restore` çalıştırılması `update`önerilir.

```cli
nuget update
```

## <a name="restore-packages"></a>Paketleri geri yükleme

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a>CLI sürümünü alın

Bu komutu kullanın:

```cli
nuget help
```

Yardım çıkışındaki ilk satır sürümü gösterir. Yukarı kaydırmayı önlemek `nuget help | more` için bunun yerine kullanın.