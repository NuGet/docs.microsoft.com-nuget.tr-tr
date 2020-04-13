---
title: Dotnet CLI'yi kullanarak NuGet paketlerini yükleyin ve yönetin
description: NuGet paketleri ile çalışmak için dotnet CLI kullanma talimatları.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 67cca81c48970c7f2e2cf0a64ee5ba57704a31e2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825167"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>Dotnet CLI kullanarak paketleri yükleme ve yönetme

CLI aracı, projelerde ve çözümlerde NuGet paketlerini kolayca yüklemenize, kaldırmanıza ve güncellemenize olanak tanır. Windows, Mac OS X ve Linux'ta çalışır.

Dotnet CLI, .NET Core ve .NET Standard projenizde (SDK tarzı proje türleri) ve diğer SDK tarzı projelerde (örneğin, .NET Framework'ü hedefleyen SDK tarzı bir proje) kullanım içindir. Daha fazla bilgi için Bkz. [SDK özniteliği.](/dotnet/core/tools/csproj#additions)

Bu makalede, en yaygın nokta CLI komutlarından birkaçı için temel kullanım gösterilmektedir. Bu komutların çoğunda CLI aracı, komutta bir proje dosyası belirtilmedikçe (proje dosyası isteğe bağlı bir anahtardır) geçerli dizinde bir proje dosyası arar. Komutların ve kullanabileceğiniz bağımsız değişkenlerin tam listesi için [.NET Core komut satırı arabirimi (CLI) araçlarına](../reference/dotnet-commands.md)bakın.

## <a name="prerequisites"></a>Ön koşullar

- Komut satırı aracını `dotnet` sağlayan [.NET Core SDK.](https://www.microsoft.com/net/download/) Visual Studio 2017'den itibaren dotnet CLI,.NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.

## <a name="install-a-package"></a>Paket yükleme

[dotnet ekle paketi](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) proje dosyasına bir paket `dotnet restore` başvurusu ekler, sonra paketi yüklemek için çalışır.

1. Bir komut satırı açın ve proje dosyanızı içeren dizine geçin.

2. Nuget paketi yüklemek için aşağıdaki komutu kullanın:

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    Örneğin, `Newtonsoft.Json` paketi yüklemek için aşağıdaki komutu kullanın

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. Komut tamamlandıktan sonra, paketin yüklü olduğundan emin olmak için proje dosyasına bakın.

   Eklenen başvuruyu `.csproj` görmek için dosyayı açabilirsiniz:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Paketin belirli bir sürümünü yükleme

Sürüm belirtilmemişse, NuGet paketin en son sürümünü yükler. Nuget paketinin belirli bir sürümünü yüklemek için [dotnet ekle paket](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) komutunu da kullanabilirsiniz:

```dotnetcli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

Örneğin, `Newtonsoft.Json` paketin 12.0.1 sürümünü eklemek için şu komutu kullanın:

```dotnetcli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a>Paket referanslarını listele

Projenizin paket başvurularını [dotnet listesi paket](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) komutunu kullanarak listeleyebilirsiniz.

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a>Paketi kaldırma

Proje dosyasından paket başvurusu kaldırmak için [dotnet kaldır paket](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) komutunu kullanın.

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

Örneğin, `Newtonsoft.Json` paketi kaldırmak için aşağıdaki komutu kullanın

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Paketi güncelleştir

NuGet, paket sürümünü (anahtar) `dotnet add package` `-v` belirtmediğiniz sürece komutu kullandığınızda paketin en son sürümünü yükler.

## <a name="restore-packages"></a>Paketleri geri yükleme

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
