---
title: dotnet CLI kullanarak NuGet paketlerini yükleme ve yönetme
description: NuGet paketleriyle çalışmak için dotnet CLI kullanma yönergeleri.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 62c05aad388c25120d5b9f5143017a2f4f3b276b
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323615"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>dotnet CLI kullanarak paketleri yükleme ve yönetme

CLI aracı, projelerde ve çözümlerde NuGet paketlerini kolayca yüklemenizi, kaldırmanızı ve güncelleştirmenizi sağlar. Windows, Mac OS X ve Linux üzerinde çalışır.

dotnet CLI, .NET Core ve .NET Standard projesinde (SDK stili proje türleri) ve diğer SDK stili projeler (örneğin, .NET Framework'i hedef alan SDK stilinde bir proje) için kullanılabilir. Daha fazla bilgi için bkz. [SDK özniteliği.](/dotnet/core/tools/csproj#additions)

Bu makalede, en yaygın dotnet CLI komutlarından birkaçı için temel kullanım bilgileri velanmıştır. Bu komutların çoğunda, komutta bir proje dosyası belirtilmemişse (proje dosyası isteğe bağlı bir anahtardır) CLI aracı geçerli dizinde bir proje dosyası olarak görünür. Kullanabileceğiniz komutların ve bağımsız değişkenlerin tam listesi için bkz. [.NET Core komut satırı arabirimi (CLI) araçları.](../reference/dotnet-commands.md)

## <a name="prerequisites"></a>Önkoşullar

- Komut [.NET Core SDK](https://www.microsoft.com/net/download/)sağlayan komut `dotnet` satırı aracı. 2017'Visual Studio itibaren dotnet CLI, .NET Core ile ilgili tüm iş yükleriyle otomatik olarak yüklenir.

## <a name="install-a-package"></a>Paketi yükleme

[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) proje dosyasına bir paket başvurusu ekler, sonra paketi `dotnet restore` yüklemek için çalıştırır.

1. Bir komut satırı açın ve proje dosyanızı içeren dizine geçiş.

2. NuGet paketini yüklemek için aşağıdaki komutu kullanın:

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    Örneğin, paketi yüklemek `Newtonsoft.Json` için aşağıdaki komutu kullanın

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. Komut tamamlandıktan sonra, paketin yüklü olduğundan emin olmak için proje dosyasına bakın.

   Eklenen başvuruya `.csproj` görmek için dosyayı açabilirsiniz:

    ```xml
    <ItemGroup>
      <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
    </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Paketin belirli bir sürümünü yükleme

Sürüm belirtilmezse NuGet paketin en son sürümünü yüklür. Bir NuGet paketinin belirli bir sürümünü yüklemek için [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) komutunu da kullanabilirsiniz:

```dotnetcli
dotnet add package <PACKAGE_NAME> --version <VERSION>
```

Örneğin, paketin 12.0.1 sürümünü eklemek `Newtonsoft.Json` için şu komutu kullanın:

```dotnetcli
dotnet add package Newtonsoft.Json --version 12.0.1
```

## <a name="list-package-references"></a>Paket başvurularını listele

dotnet list package komutunu kullanarak projenizin paket [başvurularını listeebilirsiniz.](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x)

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a>Paketi kaldırma

Proje [dosyasından paket başvurularını](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) kaldırmak için dotnet remove package komutunu kullanın.

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

Örneğin, paketi kaldırmak `Newtonsoft.Json` için aşağıdaki komutu kullanın

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Paketi güncelleştirme

NuGet, komutunu kullanarak paket sürümünü ( `dotnet add package` anahtarı) belirtmedikçe paketin en son sürümünü `-v` yüklür.

## <a name="restore-packages"></a>Paketleri geri yükleme

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
